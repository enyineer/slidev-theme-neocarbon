<!--
  NcHeatmap — GitHub-style contribution/activity heatmap.

  Usage:
    <NcHeatmap 
      :data="[0,1,2,3,4,0,1,2,0,0,4,3,2,1,0,2,3,4,4,3,2,1,0,0,1,2,3,4]"
      :columns="7"
      :headers="['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']"
      label="Activity"
    />
-->
<script setup lang="ts">
import { ref, onMounted, computed } from 'vue'

const props = withDefaults(defineProps<{
  data: number[]
  columns?: number
  label?: string
  headers?: string[]
  cellSize?: number
  colors?: string[]
}>(), {
  columns: 7,
  cellSize: 28,
  colors: () => [
    'rgba(255, 255, 255, 0.03)',
    'rgba(var(--nc-accent-rgb, 227, 6, 19), 0.15)',
    'rgba(var(--nc-accent-rgb, 227, 6, 19), 0.3)',
    'rgba(var(--nc-accent-rgb, 227, 6, 19), 0.5)',
    'rgba(var(--nc-accent-rgb, 227, 6, 19), 0.75)',
  ],
})

const visible = ref(false)
onMounted(() => { setTimeout(() => { visible.value = true }, 300) })

const maxVal = computed(() => Math.max(...props.data, 1))

function getColor(val: number) {
  if (val === 0) return props.colors[0]
  const idx = Math.min(Math.ceil((val / maxVal.value) * (props.colors.length - 1)), props.colors.length - 1)
  return props.colors[idx]
}
</script>

<template>
  <div class="nc-heatmap">
    <p v-if="label" class="nc-heatmap-label">{{ label }}</p>

    <!-- Column headers -->
    <div
      v-if="headers"
      class="nc-heatmap-headers"
      :style="{ gridTemplateColumns: `repeat(${columns}, ${cellSize}px)` }"
    >
      <span v-for="(h, i) in headers" :key="i" class="nc-heatmap-header">{{ h }}</span>
    </div>

    <!-- Grid -->
    <div
      :class="['nc-heatmap-grid', { 'nc-heatmap-visible': visible }]"
      :style="{ gridTemplateColumns: `repeat(${columns}, ${cellSize}px)` }"
    >
      <div
        v-for="(val, i) in data"
        :key="i"
        class="nc-heatmap-cell"
        :style="{
          backgroundColor: getColor(val),
          width: `${cellSize}px`,
          height: `${cellSize}px`,
          '--delay': `${0.01 * i}s`,
        }"
        :title="`Value: ${val}`"
      />
    </div>

    <!-- Legend -->
    <div class="nc-heatmap-legend">
      <span class="nc-heatmap-legend-label">Less</span>
      <div
        v-for="(color, i) in colors"
        :key="i"
        class="nc-heatmap-legend-cell"
        :style="{ backgroundColor: color }"
      />
      <span class="nc-heatmap-legend-label">More</span>
    </div>
  </div>
</template>

<style scoped>
.nc-heatmap {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 4px;
}

.nc-heatmap-label {
  font-size: 0.65rem !important;
  font-weight: 700 !important;
  text-transform: uppercase;
  letter-spacing: 0.06em;
  color: rgba(255, 255, 255, 0.35) !important;
}

.nc-heatmap-headers {
  display: grid;
  gap: 3px;
}

.nc-heatmap-header {
  font-size: 0.5rem !important;
  font-weight: 600;
  color: rgba(255, 255, 255, 0.3) !important;
  text-align: center;
  text-transform: uppercase;
  letter-spacing: 0.03em;
}

.nc-heatmap-grid {
  display: grid;
  gap: 3px;
}

.nc-heatmap-cell {
  border-radius: 3px;
  opacity: 0;
  transform: scale(0);
  transition: all 0.3s cubic-bezier(0.16, 1, 0.3, 1);
  transition-delay: var(--delay);
  cursor: pointer;
}

.nc-heatmap-visible .nc-heatmap-cell {
  opacity: 1;
  transform: scale(1);
}

.nc-heatmap-cell:hover {
  transform: scale(1.2) !important;
  box-shadow: 0 0 10px rgba(var(--nc-accent-rgb, 227, 6, 19), 0.3);
  z-index: 1;
  position: relative;
}

.nc-heatmap-legend {
  display: flex;
  align-items: center;
  gap: 3px;
  align-self: flex-end;
  margin-top: 2px;
}

.nc-heatmap-legend-label {
  font-size: 0.5rem !important;
  color: rgba(255, 255, 255, 0.25) !important;
  margin: 0 2px;
}

.nc-heatmap-legend-cell {
  width: 10px;
  height: 10px;
  border-radius: 2px;
}
</style>
