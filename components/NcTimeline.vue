<!--
  NcTimeline — Horizontal or vertical timeline with animated nodes.
  
  Usage:
    <NcTimeline :items="[
      { label: 'Q1', title: 'Research', description: 'Market analysis', color: '#E30613' },
      { label: 'Q2', title: 'Build', description: 'MVP development', color: '#ff4444' },
      { label: 'Q3', title: 'Launch', description: 'Go to market', color: '#4ade80', active: true },
    ]" />
-->
<script setup lang="ts">
import { ref, onMounted } from 'vue'

interface TimelineItem {
  label?: string
  title: string
  description?: string
  color?: string
  active?: boolean
}

defineProps<{
  items: TimelineItem[]
  vertical?: boolean
}>()

const visible = ref(false)
onMounted(() => {
  setTimeout(() => { visible.value = true }, 200)
})
</script>

<template>
  <div :class="['nc-timeline', { 'nc-timeline-vertical': vertical, 'nc-timeline-visible': visible }]">
    <div
      v-for="(item, i) in items"
      :key="i"
      class="nc-tl-item"
      :style="{ '--delay': `${0.15 + i * 0.12}s`, '--color': item.color || 'var(--nc-accent, #E30613)' }"
    >
      <!-- Node dot -->
      <div :class="['nc-tl-node', { 'nc-tl-active': item.active }]">
        <div class="nc-tl-dot" />
        <div v-if="item.active" class="nc-tl-pulse" />
      </div>

      <!-- Content -->
      <div class="nc-tl-content">
        <span v-if="item.label" class="nc-tl-label">{{ item.label }}</span>
        <p class="nc-tl-title">{{ item.title }}</p>
        <p v-if="item.description" class="nc-tl-desc">{{ item.description }}</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
/* ===== HORIZONTAL (default) ===== */
.nc-timeline {
  display: flex;
  align-items: flex-start;
  gap: 0;
  width: 100%;
  position: relative;
}

.nc-tl-item {
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  position: relative;
  opacity: 0;
  transform: translateY(12px);
  transition: all 0.6s cubic-bezier(0.16, 1, 0.3, 1);
  transition-delay: var(--delay);
}

.nc-timeline-visible .nc-tl-item {
  opacity: 1;
  transform: translateY(0);
}

/* Connector line */
.nc-tl-item:not(:last-child)::after {
  content: '';
  position: absolute;
  top: 9px;
  left: calc(50% + 12px);
  right: calc(-50% + 12px);
  height: 2px;
  background: rgba(255, 255, 255, 0.08);
}

.nc-tl-node {
  position: relative;
  width: 20px;
  height: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 10px;
  z-index: 1;
}

.nc-tl-dot {
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background: var(--color);
  box-shadow: 0 0 12px var(--color);
  transition: transform 0.3s ease;
}

.nc-tl-active .nc-tl-dot {
  width: 14px;
  height: 14px;
}

.nc-tl-pulse {
  position: absolute;
  width: 24px;
  height: 24px;
  border-radius: 50%;
  border: 2px solid var(--color);
  opacity: 0;
  animation: nc-tl-ping 2s cubic-bezier(0, 0, 0.2, 1) infinite;
}

@keyframes nc-tl-ping {
  0% { transform: scale(0.8); opacity: 0.6; }
  100% { transform: scale(1.8); opacity: 0; }
}

.nc-tl-label {
  font-size: 0.55rem;
  font-weight: 700;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: var(--color);
  margin-bottom: 2px;
}

.nc-tl-title {
  font-size: 0.75rem !important;
  font-weight: 700;
  color: white !important;
}

.nc-tl-desc {
  font-size: 0.6rem !important;
  color: rgba(255, 255, 255, 0.35) !important;
  margin-top: 2px;
  max-width: 120px;
}

/* ===== VERTICAL ===== */
.nc-timeline-vertical {
  flex-direction: column;
  gap: 0.5rem;
}

.nc-timeline-vertical .nc-tl-item {
  flex-direction: row;
  align-items: flex-start;
  text-align: left;
}

.nc-timeline-vertical .nc-tl-item:not(:last-child)::after {
  top: 20px;
  left: 9px;
  right: auto;
  width: 2px;
  height: calc(100% + 0.5rem);
}

.nc-timeline-vertical .nc-tl-node {
  margin-bottom: 0;
  margin-right: 12px;
  flex-shrink: 0;
}

.nc-timeline-vertical .nc-tl-content {
  padding-top: 1px;
}

.nc-timeline-vertical .nc-tl-desc {
  max-width: none;
}
</style>
