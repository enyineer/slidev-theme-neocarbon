<!--
  NcCallout — Styled callout/alert box with icon, accent border, and content.
  
  Usage:
    <NcCallout type="info" title="Did you know?">
      This is an informational callout with an icon and styled border.
    </NcCallout>
-->
<script setup lang="ts">
defineProps<{
  type?: 'info' | 'success' | 'warning' | 'danger' | 'accent'
  title?: string
  icon?: string
}>()

const icons: Record<string, string> = {
  info: 'ℹ️',
  success: '✅',
  warning: '⚠️',
  danger: '🚨',
  accent: '💡',
}

const colorMap: Record<string, string> = {
  info: 'var(--nc-info, #60a5fa)',
  success: 'var(--nc-success, #4ade80)',
  warning: 'var(--nc-warning, #fbbf24)',
  danger: 'var(--nc-danger, #ea580c)',
  accent: 'var(--nc-accent, #E30613)',
}
</script>

<template>
  <div
    class="nc-callout"
    :style="{
      '--callout-color': colorMap[type || 'accent'],
    }"
  >
    <div class="nc-callout-icon">
      {{ icon || icons[type || 'accent'] }}
    </div>
    <div class="nc-callout-body">
      <p v-if="title" class="nc-callout-title">{{ title }}</p>
      <div class="nc-callout-content">
        <slot />
      </div>
    </div>
  </div>
</template>

<style scoped>
.nc-callout {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 12px 16px;
  border-radius: 12px;
  background: rgba(255, 255, 255, 0.03);
  border: 1px solid rgba(255, 255, 255, 0.06);
  border-left: 3px solid var(--callout-color);
  position: relative;
  overflow: hidden;
}

/* Subtle glow on the left border */
.nc-callout::before {
  content: '';
  position: absolute;
  left: -1px;
  top: 0;
  bottom: 0;
  width: 60px;
  background: linear-gradient(90deg, var(--callout-color), transparent);
  opacity: 0.05;
  pointer-events: none;
}

.nc-callout-icon {
  font-size: 1rem;
  flex-shrink: 0;
  margin-top: 1px;
}

.nc-callout-title {
  font-size: 0.75rem !important;
  font-weight: 700 !important;
  color: var(--callout-color) !important;
  margin-bottom: 2px;
}

.nc-callout-content {
  font-size: 0.68rem !important;
  color: var(--nc-text-muted) !important;
  line-height: 1.5;
}

.nc-callout-content :deep(strong) {
  color: white !important;
}

.nc-callout-content :deep(code) {
  background: rgba(255, 255, 255, 0.08);
  padding: 1px 5px;
  border-radius: 4px;
  font-size: 0.62rem;
}
</style>
