<!--
  NcRoiCard — Premium ROI / financial metric card with gradient hero value,
  structured metrics, and ambient glow.

  Usage:
    <NcRoiCard
      label="Konservativ (10%)"
      source="GitHub/Microsoft-Studie: 8–13% bei Senior-Devs"
      roi="6,2×"
      color="#fbbf24"
      :metrics="[
        { label: 'Einsparung/Jahr', value: '15,84 Mio. €' },
        { label: 'Einsparung/3J', value: '47,5 Mio. €' },
      ]"
    />
-->
<script setup lang="ts">
defineProps<{
  label: string
  source?: string
  roi: string
  color?: string
  icon?: string
  metrics?: Array<{ label: string; value: string }>
}>()
</script>

<template>
  <div
    class="nc-roi-card"
    :style="{
      '--roi-color': color || 'var(--nc-accent, #E30613)',
    }"
  >


    <!-- Header -->
    <div class="nc-roi-header">
      <span v-if="icon" class="nc-roi-icon">{{ icon }}</span>
      <span class="nc-roi-label">{{ label }}</span>
    </div>

    <!-- Source -->
    <p v-if="source" class="nc-roi-source">{{ source }}</p>

    <!-- Metrics -->
    <div v-if="metrics?.length" class="nc-roi-metrics">
      <div v-for="m in metrics" :key="m.label" class="nc-roi-metric">
        <span class="nc-roi-metric-label">{{ m.label }}</span>
        <span class="nc-roi-metric-value">{{ m.value }}</span>
      </div>
    </div>

    <!-- Hero ROI value -->
    <div class="nc-roi-hero">
      <span class="nc-roi-prefix">ROI</span>
      <span class="nc-roi-value">{{ roi }}</span>
    </div>
  </div>
</template>

<style scoped>
.nc-roi-card {
  position: relative;
  display: flex;
  flex-direction: column;
  padding: 1.25rem;
  border-radius: 16px;
  background: linear-gradient(
    145deg,
    rgba(255, 255, 255, 0.04) 0%,
    rgba(255, 255, 255, 0.01) 100%
  );
  border: 1px solid rgba(255, 255, 255, 0.06);
  border-left: 3px solid var(--roi-color);
  overflow: hidden;
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.nc-roi-card:hover {
  transform: translateY(-1px);
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
}

/* Ambient corner glow via pseudo-element */
.nc-roi-card::after {
  content: '';
  position: absolute;
  bottom: 0;
  right: 0;
  width: 120px;
  height: 120px;
  background: radial-gradient(circle at 100% 100%, color-mix(in srgb, var(--roi-color) 8%, transparent), transparent 70%);
  pointer-events: none;
  border-radius: 0 0 16px 0;
}

.nc-roi-header {
  display: flex;
  align-items: center;
  gap: 6px;
}

.nc-roi-icon {
  font-size: 0.85rem;
}

.nc-roi-label {
  font-size: 0.78rem;
  font-weight: 700;
  color: var(--roi-color);
  letter-spacing: 0.02em;
}

.nc-roi-source {
  font-size: 0.52rem !important;
  color: var(--nc-text-muted) !important;
  margin-top: 4px;
  line-height: 1.4;
}

.nc-roi-metrics {
  display: flex;
  flex-direction: column;
  gap: 4px;
  margin-top: 12px;
  padding-top: 10px;
  border-top: 1px solid rgba(255, 255, 255, 0.06);
}

.nc-roi-metric {
  display: flex;
  justify-content: space-between;
  align-items: baseline;
}

.nc-roi-metric-label {
  font-size: 0.62rem;
  color: var(--nc-text-muted);
}

.nc-roi-metric-value {
  font-size: 0.68rem;
  font-weight: 700;
  color: var(--roi-color);
}

.nc-roi-hero {
  display: flex;
  align-items: baseline;
  gap: 8px;
  margin-top: auto;
  padding-top: 12px;
}

.nc-roi-prefix {
  font-size: 0.7rem;
  font-weight: 600;
  color: var(--nc-text-muted);
  text-transform: uppercase;
  letter-spacing: 0.08em;
}

.nc-roi-value {
  font-size: 1.6rem;
  font-weight: 900;
  background: linear-gradient(135deg, var(--roi-color), white);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  line-height: 1;
}
</style>
