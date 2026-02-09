<!--
  NcRadarChart — Spider/radar chart using pure SVG (no Chart.js needed).

  Usage:
    <NcRadarChart
      :labels="['Speed', 'Security', 'Scale', 'Cost', 'UX', 'DevEx']"
      :datasets="[
        { label: 'Current', data: [3, 5, 2, 4, 3, 2], color: '#ff4444' },
        { label: 'Target', data: [5, 5, 5, 4, 5, 5], color: '#4ade80' },
      ]"
    />
-->
<script setup lang="ts">
import { computed, ref, onMounted } from 'vue'

interface RadarDataset {
  label?: string
  data: number[]
  color?: string
}

const props = withDefaults(defineProps<{
  labels: string[]
  datasets: RadarDataset[]
  max?: number
  size?: number
  levels?: number
}>(), {
  max: 5,
  size: 220,
  levels: 5,
})

const visible = ref(false)
onMounted(() => { setTimeout(() => { visible.value = true }, 300) })

const padding = 50
const svgSize = computed(() => props.size + padding * 2)
const cx = computed(() => svgSize.value / 2)
const cy = computed(() => svgSize.value / 2)
const radius = computed(() => props.size / 2 - 10)

function polarToCartesian(angle: number, r: number) {
  const rad = (angle - 90) * (Math.PI / 180)
  return {
    x: cx.value + r * Math.cos(rad),
    y: cy.value + r * Math.sin(rad),
  }
}

function getPolygonPoints(data: number[]) {
  const count = props.labels.length
  return data
    .map((val, i) => {
      const angle = (360 / count) * i
      const r = (val / props.max) * radius.value
      const { x, y } = polarToCartesian(angle, r)
      return `${x},${y}`
    })
    .join(' ')
}

function getAxisEnd(index: number) {
  const angle = (360 / props.labels.length) * index
  return polarToCartesian(angle, radius.value)
}

function getLabelPosition(index: number) {
  const angle = (360 / props.labels.length) * index
  return polarToCartesian(angle, radius.value + 20)
}

function getLabelAnchor(index: number) {
  const angle = ((360 / props.labels.length) * index) % 360
  if (angle > 30 && angle < 150) return 'start'
  if (angle > 210 && angle < 330) return 'end'
  return 'middle'
}

function getLevelPoints(level: number) {
  const count = props.labels.length
  const r = (level / props.levels) * radius.value
  return Array.from({ length: count }, (_, i) => {
    const angle = (360 / count) * i
    const { x, y } = polarToCartesian(angle, r)
    return `${x},${y}`
  }).join(' ')
}
</script>

<template>
  <div :class="['nc-radar', { 'nc-radar-visible': visible }]">
    <svg :width="size" :height="size" :viewBox="`0 0 ${svgSize} ${svgSize}`" overflow="visible">
      <!-- Grid levels -->
      <polygon
        v-for="l in levels"
        :key="'level-' + l"
        :points="getLevelPoints(l)"
        fill="none"
        :stroke="l === levels ? 'rgba(255,255,255,0.1)' : 'rgba(255,255,255,0.04)'"
        stroke-width="1"
      />

      <!-- Axes -->
      <line
        v-for="(_, i) in labels"
        :key="'axis-' + i"
        :x1="cx"
        :y1="cy"
        :x2="getAxisEnd(i).x"
        :y2="getAxisEnd(i).y"
        stroke="rgba(255,255,255,0.06)"
        stroke-width="1"
      />

      <!-- Data polygons -->
      <polygon
        v-for="(ds, di) in datasets"
        :key="'data-' + di"
        :points="getPolygonPoints(ds.data)"
        :fill="(ds.color || '#E30613') + '18'"
        :stroke="ds.color || '#E30613'"
        stroke-width="2"
        class="nc-radar-polygon"
        :style="{ '--delay': `${0.3 + di * 0.15}s` }"
      />

      <!-- Data points -->
      <template v-for="(ds, di) in datasets" :key="'dots-' + di">
        <circle
          v-for="(val, vi) in ds.data"
          :key="'dot-' + di + '-' + vi"
          :cx="polarToCartesian((360 / labels.length) * vi, (val / max) * radius).x"
          :cy="polarToCartesian((360 / labels.length) * vi, (val / max) * radius).y"
          r="3"
          :fill="ds.color || '#E30613'"
          class="nc-radar-dot"
          :style="{ '--delay': `${0.4 + di * 0.15 + vi * 0.03}s` }"
        />
      </template>

      <!-- Labels -->
      <text
        v-for="(label, i) in labels"
        :key="'label-' + i"
        :x="getLabelPosition(i).x"
        :y="getLabelPosition(i).y"
        :text-anchor="getLabelAnchor(i)"
        dominant-baseline="central"
        fill="rgba(255,255,255,0.45)"
        font-size="7"
        font-weight="600"
        font-family="Inter, system-ui, sans-serif"
      >
        {{ label }}
      </text>
    </svg>

    <!-- Legend -->
    <div v-if="datasets.some(d => d.label)" class="nc-radar-legend">
      <div v-for="(ds, i) in datasets" :key="i" class="nc-radar-legend-item">
        <span class="nc-radar-legend-dot" :style="{ background: ds.color || '#E30613' }" />
        <span>{{ ds.label }}</span>
      </div>
    </div>
  </div>
</template>

<style scoped>
.nc-radar {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 8px;
  overflow: visible;
}

.nc-radar-polygon {
  opacity: 0;
  transition: opacity 0.6s ease;
  transition-delay: var(--delay);
}

.nc-radar-visible .nc-radar-polygon {
  opacity: 1;
}

.nc-radar-dot {
  opacity: 0;
  transition: opacity 0.4s ease;
  transition-delay: var(--delay);
}

.nc-radar-visible .nc-radar-dot {
  opacity: 1;
}

.nc-radar-legend {
  display: flex;
  gap: 12px;
}

.nc-radar-legend-item {
  display: flex;
  align-items: center;
  gap: 4px;
  font-size: 0.6rem;
  color: rgba(255, 255, 255, 0.5);
  font-weight: 600;
}

.nc-radar-legend-dot {
  width: 8px;
  height: 8px;
  border-radius: 50%;
}
</style>
