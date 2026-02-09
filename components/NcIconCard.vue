<!--
  NcIconCard — A styled card with an icon badge, title, and optional description.

  Usage with slot icon (recommended for Carbon icons):
    <NcIconCard title="Lightning Fast" description="Sub-second response times">
      <template #icon><carbon-flash /></template>
    </NcIconCard>

  Usage with emoji prop:
    <NcIconCard icon="🚀" title="Ready to Launch" />
-->
<script setup lang="ts">
defineProps<{
  icon?: string;
  title: string;
  description?: string;
  color?: string;
  highlighted?: boolean;
  small?: boolean;
}>();
</script>

<template>
  <div :class="['nc-icon-card', { 'nc-icon-card-highlight': highlighted }]">
    <div
      v-if="icon || $slots.icon"
      :class="small ? 'nc-icon-sm' : 'nc-icon'"
      :style="
        color ? { background: color, boxShadow: `0 4px 15px ${color}40` } : {}
      "
    >
      <slot name="icon">
        <span class="nc-icon-emoji">{{ icon }}</span>
      </slot>
    </div>
    <div class="nc-icon-card-body">
      <p class="nc-icon-card-title">{{ title }}</p>
      <p v-if="description" class="nc-icon-card-desc">{{ description }}</p>
      <slot />
    </div>
  </div>
</template>

<style scoped>
.nc-icon-card {
  display: flex;
  align-items: flex-start;
  gap: 12px;
  padding: 12px 14px;
  border-radius: 14px;
  background: var(--nc-surface, #161616);
  border: 1px solid var(--nc-border, rgba(255, 255, 255, 0.06));
  transition:
    transform 0.3s ease,
    box-shadow 0.3s ease,
    border-color 0.3s ease;
}

.nc-icon-card:hover {
  transform: translateY(-1px);
  border-color: rgba(var(--nc-accent-rgb, 227, 6, 19), 0.15);
  box-shadow: 0 4px 20px rgba(var(--nc-accent-rgb, 227, 6, 19), 0.08);
}

.nc-icon-card-highlight {
  background: linear-gradient(
    135deg,
    rgba(var(--nc-accent-rgb, 227, 6, 19), 0.1),
    rgba(var(--nc-accent-rgb, 227, 6, 19), 0.03)
  ) !important;
  border-color: rgba(var(--nc-accent-rgb, 227, 6, 19), 0.2);
}

.nc-icon-card-title {
  font-size: 0.78rem !important;
  font-weight: 700 !important;
  color: white !important;
}

.nc-icon-card-desc {
  font-size: 0.65rem !important;
  color: rgba(255, 255, 255, 0.4) !important;
  margin-top: 2px;
  line-height: 1.5;
}

.nc-icon-emoji {
  font-size: 16px;
  line-height: 1;
  font-family: 'Apple Color Emoji', 'Segoe UI Emoji', 'Noto Color Emoji', sans-serif !important;
}

.nc-icon :deep(svg) {
  width: 16px;
  height: 16px;
  color: white;
}
</style>
