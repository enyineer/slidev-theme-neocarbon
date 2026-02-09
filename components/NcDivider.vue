<!--
  NcDivider — A themed horizontal divider with optional label text.

  Usage:
    <NcDivider />
    <NcDivider label="OR" />
    <NcDivider label="Section" accent />
-->
<script setup lang="ts">
defineProps<{
  label?: string
  accent?: boolean
}>()
</script>

<template>
  <div :class="['nc-divider', { 'nc-divider-accent': accent }]">
    <div class="nc-divider-line" />
    <span v-if="label" class="nc-divider-label">{{ label }}</span>
    <div v-if="label" class="nc-divider-line" />
  </div>
</template>

<style scoped>
.nc-divider {
  display: flex;
  align-items: center;
  gap: 12px;
  margin: 0.5rem 0;
}

.nc-divider-line {
  flex: 1;
  height: 1px;
  background: linear-gradient(
    90deg,
    transparent,
    rgba(255, 255, 255, 0.08) 30%,
    rgba(255, 255, 255, 0.08) 70%,
    transparent
  );
}

.nc-divider-accent .nc-divider-line {
  background: linear-gradient(
    90deg,
    transparent,
    rgba(var(--nc-accent-rgb, 227, 6, 19), 0.2) 30%,
    rgba(var(--nc-accent-rgb, 227, 6, 19), 0.2) 70%,
    transparent
  );
}

.nc-divider-label {
  font-size: 0.55rem;
  font-weight: 700;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: rgba(255, 255, 255, 0.25);
  white-space: nowrap;
}

.nc-divider-accent .nc-divider-label {
  color: var(--nc-accent, #E30613);
}
</style>
