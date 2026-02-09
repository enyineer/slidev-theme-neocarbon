<!--
  NcTicker — Financial-style ticker showing values with up/down indicators.
  Pairs beautifully with the marquee for a Bloomberg-terminal aesthetic.

  Usage:
    <NcTicker :items="[
      { label: 'Revenue', value: '47.5M', change: 12.4 },
      { label: 'Users', value: '42K', change: 8.2 },
      { label: 'Latency', value: '3.2ms', change: -15.1 },
    ]" />
-->
<script setup lang="ts">
import { ref, onMounted } from 'vue'

interface TickerItem {
  label: string
  value: string
  change?: number
  unit?: string
}

const props = defineProps<{
  items: TickerItem[]
}>()

const visible = ref(false)
onMounted(() => { setTimeout(() => { visible.value = true }, 200) })
</script>

<template>
  <div :class="['nc-ticker', { 'nc-ticker-visible': visible }]">
    <div
      v-for="(item, i) in items"
      :key="i"
      class="nc-ticker-item"
      :style="{ '--delay': `${0.08 * i}s` }"
    >
      <span class="nc-ticker-label">{{ item.label }}</span>
      <span class="nc-ticker-value">{{ item.value }}{{ item.unit || '' }}</span>
      <span
        v-if="item.change !== undefined"
        :class="['nc-ticker-change', item.change >= 0 ? 'nc-ticker-up' : 'nc-ticker-down']"
      >
        {{ item.change >= 0 ? '▲' : '▼' }}
        {{ Math.abs(item.change).toFixed(1) }}%
      </span>
    </div>
  </div>
</template>

<style scoped>
.nc-ticker {
  display: flex;
  gap: 2px;
  overflow: hidden;
  border-radius: 10px;
  border: 1px solid rgba(255, 255, 255, 0.06);
  background: var(--nc-surface, #161616);
}

.nc-ticker-item {
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 10px 12px;
  gap: 2px;
  border-right: 1px solid rgba(255, 255, 255, 0.04);
  opacity: 0;
  transform: translateY(8px);
  transition: all 0.5s cubic-bezier(0.16, 1, 0.3, 1);
  transition-delay: var(--delay);
}

.nc-ticker-visible .nc-ticker-item {
  opacity: 1;
  transform: translateY(0);
}

.nc-ticker-item:last-child {
  border-right: none;
}

.nc-ticker-label {
  font-size: 0.55rem !important;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.06em;
  color: rgba(255, 255, 255, 0.3);
}

.nc-ticker-value {
  font-size: 0.9rem !important;
  font-weight: 800 !important;
  color: white;
  font-variant-numeric: tabular-nums;
}

.nc-ticker-change {
  font-size: 0.55rem !important;
  font-weight: 700;
  font-variant-numeric: tabular-nums;
  padding: 1px 6px;
  border-radius: 4px;
}

.nc-ticker-up {
  color: var(--nc-success, #4ade80);
  background: rgba(74, 222, 128, 0.08);
}

.nc-ticker-down {
  color: var(--nc-danger, #ea580c);
  background: rgba(234, 88, 12, 0.08);
}
</style>
