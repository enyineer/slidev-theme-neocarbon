<!--
  NcFeatureGrid — Auto-layout grid of feature items with icons.
  Reduces boilerplate for the most common slide pattern.

  Usage:
    <NcFeatureGrid :features="[
      { icon: '🚀', title: 'Fast', description: 'Sub-second builds' },
      { icon: '🔒', title: 'Secure', description: 'Zero-trust architecture' },
      { icon: '📊', title: 'Analytics', description: 'Real-time dashboards' },
      { icon: '🌍', title: 'Global', description: 'Edge deployment' },
    ]" />
-->
<script setup lang="ts">
import { ref, onMounted } from 'vue'

interface Feature {
  icon?: string
  title: string
  description?: string
  color?: string
}

defineProps<{
  features: Feature[]
  columns?: number
}>()

const visible = ref(false)
onMounted(() => { setTimeout(() => { visible.value = true }, 200) })
</script>

<template>
  <div
    :class="['nc-feat-grid', { 'nc-feat-visible': visible }]"
    :style="{ gridTemplateColumns: `repeat(${columns || Math.min(features.length, 3)}, 1fr)` }"
  >
    <div
      v-for="(feat, i) in features"
      :key="i"
      class="nc-feat-item"
      :style="{ '--delay': `${0.1 + i * 0.08}s` }"
    >
      <div v-if="feat.icon" class="nc-feat-icon" :style="feat.color ? { background: feat.color + '20', boxShadow: `0 0 20px ${feat.color}30` } : {}">
        {{ feat.icon }}
      </div>
      <p class="nc-feat-title">{{ feat.title }}</p>
      <p v-if="feat.description" class="nc-feat-desc">{{ feat.description }}</p>
    </div>
  </div>
</template>

<style scoped>
.nc-feat-grid {
  display: grid;
  gap: 0.75rem;
  width: 100%;
}

.nc-feat-item {
  background: var(--nc-surface, #161616);
  border: 1px solid var(--nc-border, rgba(255, 255, 255, 0.06));
  border-radius: 14px;
  padding: 16px;
  text-align: center;
  opacity: 0;
  transform: translateY(14px) scale(0.96);
  transition: all 0.5s cubic-bezier(0.16, 1, 0.3, 1);
  transition-delay: var(--delay);
}

.nc-feat-visible .nc-feat-item {
  opacity: 1;
  transform: translateY(0) scale(1);
}

.nc-feat-item:hover {
  transform: translateY(-2px) !important;
  border-color: rgba(var(--nc-accent-rgb, 227, 6, 19), 0.15);
  box-shadow: 0 8px 30px rgba(0, 0, 0, 0.3);
}

.nc-feat-icon {
  font-size: 1.5rem;
  width: 48px;
  height: 48px;
  border-radius: 14px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0 auto 10px;
  background: rgba(var(--nc-accent-rgb, 227, 6, 19), 0.1);
  box-shadow: 0 0 20px rgba(var(--nc-accent-rgb, 227, 6, 19), 0.1);
}

.nc-feat-title {
  font-size: 0.78rem !important;
  font-weight: 700 !important;
  color: white !important;
}

.nc-feat-desc {
  font-size: 0.6rem !important;
  color: rgba(255, 255, 255, 0.35) !important;
  margin-top: 4px;
  line-height: 1.5;
}
</style>
