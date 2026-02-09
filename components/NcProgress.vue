<!--
  NcProgress — Animated progress/skill bar
  
  Usage:
    <NcProgress label="TypeScript" :value="92" color="var(--nc-accent)" />
-->
<script setup lang="ts">
import { ref, onMounted } from 'vue'

const props = defineProps<{
  label?: string
  value: number
  color?: string
  showValue?: boolean
}>()

const animatedWidth = ref(0)
const displayValue = ref(0)

onMounted(() => {
  requestAnimationFrame(() => {
    setTimeout(() => {
      const duration = 1200
      const start = performance.now()
      function tick(now: number) {
        const progress = Math.min((now - start) / duration, 1)
        const eased = 1 - Math.pow(1 - progress, 3)
        animatedWidth.value = eased * props.value
        displayValue.value = Math.round(eased * props.value)
        if (progress < 1) requestAnimationFrame(tick)
      }
      requestAnimationFrame(tick)
    }, 300)
  })
})
</script>

<template>
  <div class="nc-progress-wrap">
    <div v-if="label || showValue !== false" class="nc-progress-header">
      <span v-if="label" class="nc-progress-label">{{ label }}</span>
      <span v-if="showValue !== false" class="nc-progress-value">{{ displayValue }}%</span>
    </div>
    <div class="nc-progress-track">
      <div
        class="nc-progress-fill"
        :style="{
          width: animatedWidth + '%',
          background: color || 'var(--nc-accent, #E30613)',
          boxShadow: `0 0 12px ${color || 'rgba(var(--nc-accent-rgb, 227, 6, 19), 0.5)'}`,
        }"
      />
    </div>
  </div>
</template>

<style scoped>
.nc-progress-wrap {
  width: 100%;
}

.nc-progress-header {
  display: flex;
  justify-content: space-between;
  align-items: baseline;
  margin-bottom: 4px;
}

.nc-progress-label {
  font-size: 0.7rem;
  font-weight: 600;
  color: white;
}

.nc-progress-value {
  font-size: 0.65rem;
  font-weight: 700;
  color: rgba(255, 255, 255, 0.5);
  font-variant-numeric: tabular-nums;
}

.nc-progress-track {
  width: 100%;
  height: 6px;
  background: rgba(255, 255, 255, 0.06);
  border-radius: 6px;
  overflow: hidden;
}

.nc-progress-fill {
  height: 100%;
  border-radius: 6px;
  transition: width 0.05s linear;
  position: relative;
}

/* Shimmer on the fill */
.nc-progress-fill::after {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(
    90deg,
    transparent 0%,
    rgba(255, 255, 255, 0.15) 50%,
    transparent 100%
  );
  animation: nc-progress-shimmer 2s ease-in-out infinite;
}

@keyframes nc-progress-shimmer {
  0% { transform: translateX(-100%); }
  100% { transform: translateX(200%); }
}
</style>
