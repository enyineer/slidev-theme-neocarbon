<!--
  NcBadge — Small status badge / tag pill.

  Usage:
    <NcBadge>Done</NcBadge>
    <NcBadge type="warning">In Progress</NcBadge>
    <NcBadge type="danger" glow>Critical</NcBadge>
-->
<script setup lang="ts">
defineProps<{
  type?: 'accent' | 'success' | 'warning' | 'danger' | 'info' | 'neutral'
  glow?: boolean
}>()

const colorMap: Record<string, { bg: string; text: string; shadow: string }> = {
  accent:  { bg: 'rgba(var(--nc-accent-rgb, 227, 6, 19), 0.15)', text: 'var(--nc-accent, #E30613)', shadow: 'rgba(var(--nc-accent-rgb, 227, 6, 19), 0.4)' },
  success: { bg: 'rgba(74, 222, 128, 0.12)', text: 'var(--nc-success, #4ade80)', shadow: 'rgba(74, 222, 128, 0.4)' },
  warning: { bg: 'rgba(251, 191, 36, 0.12)', text: 'var(--nc-warning, #fbbf24)', shadow: 'rgba(251, 191, 36, 0.4)' },
  danger:  { bg: 'rgba(234, 88, 12, 0.12)', text: 'var(--nc-danger, #ea580c)', shadow: 'rgba(234, 88, 12, 0.4)' },
  info:    { bg: 'rgba(96, 165, 250, 0.12)', text: 'var(--nc-info, #60a5fa)', shadow: 'rgba(96, 165, 250, 0.4)' },
  neutral: { bg: 'rgba(255, 255, 255, 0.06)', text: 'rgba(255, 255, 255, 0.6)', shadow: 'transparent' },
}
</script>

<template>
  <span
    class="nc-badge"
    :style="{
      background: colorMap[type || 'accent'].bg,
      color: colorMap[type || 'accent'].text,
      boxShadow: glow ? `0 0 12px ${colorMap[type || 'accent'].shadow}` : 'none',
    }"
  >
    <slot />
  </span>
</template>

<style scoped>
.nc-badge {
  display: inline-flex;
  align-items: center;
  padding: 2px 10px;
  border-radius: 100px;
  font-size: 0.6rem;
  font-weight: 700;
  letter-spacing: 0.03em;
  text-transform: uppercase;
  white-space: nowrap;
  line-height: 1.6;
}
</style>
