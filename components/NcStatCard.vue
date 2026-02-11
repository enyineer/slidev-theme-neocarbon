<!--
  NcStatCard — Pre-styled statistic/KPI card with animated value.

  Usage:
    <NcStatCard value="47.5M €" label="Savings" color="var(--nc-success)" />
    <NcStatCard value="99.9%" label="Uptime" borderColor="var(--nc-accent)" />
    <NcStatCard value="7.7M €" label="Total TCO" highlighted />
-->
<script setup lang="ts">
defineProps<{
  value: string;
  label: string;
  color?: string;
  borderColor?: string;
  icon?: string;
  highlighted?: boolean;
}>();
</script>

<template>
  <div
    :class="['nc-stat-card', { 'nc-stat-highlight': highlighted }]"
    :style="{
      borderTopColor: borderColor || color || 'var(--nc-accent, #E30613)',
    }"
  >
    <span v-if="icon" class="nc-stat-icon">{{ icon }}</span>
    <slot>
      <p class="nc-stat-value" :style="{ '--nc-stat-color': color || 'white' }">
        {{ value }}
      </p>
    </slot>
    <p class="nc-stat-label">{{ label }}</p>
  </div>
</template>

<style scoped>
.nc-stat-card {
  background: var(--nc-surface, #161616);
  border: 1px solid var(--nc-border, rgba(255, 255, 255, 0.06));
  border-top: 2px solid var(--nc-accent, #e30613);
  border-radius: 14px;
  padding: 12px 16px;
  text-align: center;
  transition:
    transform 0.3s ease,
    box-shadow 0.3s ease;
  animation: nc-stat-enter 0.6s cubic-bezier(0.16, 1, 0.3, 1) both;
}

.nc-stat-card:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 25px rgba(0, 0, 0, 0.3);
}

.nc-stat-highlight {
  background: linear-gradient(
    135deg,
    rgba(var(--nc-accent-rgb, 227, 6, 19), 0.12),
    rgba(var(--nc-accent-rgb, 227, 6, 19), 0.04)
  ) !important;
  border-color: rgba(var(--nc-accent-rgb, 227, 6, 19), 0.25);
  box-shadow: 0 0 30px rgba(var(--nc-accent-rgb, 227, 6, 19), 0.08);
  position: relative;
  overflow: hidden;
}

.nc-stat-highlight::after {
  content: "";
  position: absolute;
  top: -50%;
  left: -50%;
  width: 200%;
  height: 200%;
  background: linear-gradient(
    115deg,
    transparent 40%,
    rgba(255, 255, 255, 0.03) 45%,
    rgba(255, 255, 255, 0.06) 50%,
    rgba(255, 255, 255, 0.03) 55%,
    transparent 60%
  );
  animation: nc-shimmer 6s ease-in-out infinite;
  pointer-events: none;
}

.nc-stat-icon {
  font-size: 1.2rem;
  display: block;
  margin-bottom: 4px;
}

.nc-stat-value {
  font-size: 1.1rem !important;
  font-weight: 900 !important;
  font-variant-numeric: tabular-nums;
  color: var(--nc-stat-color, white) !important;
}

.nc-stat-label {
  font-size: 0.6rem !important;
  color: var(--nc-text-muted) !important;
  margin-top: 2px;
}

@keyframes nc-stat-enter {
  from {
    opacity: 0;
    transform: translateY(10px) scale(0.96);
  }
  to {
    opacity: 1;
    transform: translateY(0) scale(1);
  }
}

@keyframes nc-shimmer {
  0%,
  100% {
    transform: translateX(-100%) rotate(0deg);
  }
  50% {
    transform: translateX(100%) rotate(0deg);
  }
}
</style>
