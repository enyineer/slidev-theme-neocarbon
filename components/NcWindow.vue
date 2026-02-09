<!--
  NcWindow — macOS-style window chrome wrapper.
  Wraps any content in a window with traffic-light dots and optional title.

  Usage:
    <NcWindow title="api-handler.ts">
      <pre>const x = 42;</pre>
    </NcWindow>
-->
<script setup lang="ts">
defineProps<{
  title?: string
  dark?: boolean
}>()
</script>

<template>
  <div :class="['nc-window', { 'nc-window-dark': dark }]">
    <div class="nc-window-bar">
      <div class="nc-window-dots">
        <span class="nc-wdot nc-wdot-r" />
        <span class="nc-wdot nc-wdot-y" />
        <span class="nc-wdot nc-wdot-g" />
      </div>
      <span v-if="title" class="nc-window-title">{{ title }}</span>
    </div>
    <div class="nc-window-body">
      <slot />
    </div>
  </div>
</template>

<style scoped>
.nc-window {
  border-radius: 14px;
  overflow: hidden;
  border: 1px solid rgba(255, 255, 255, 0.08);
  box-shadow:
    0 20px 60px rgba(0, 0, 0, 0.4),
    0 0 1px rgba(255, 255, 255, 0.1);
  animation: nc-win-enter 0.6s cubic-bezier(0.16, 1, 0.3, 1) both;
}

@keyframes nc-win-enter {
  from { opacity: 0; transform: translateY(10px) scale(0.97); }
  to { opacity: 1; transform: translateY(0) scale(1); }
}

.nc-window-bar {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 10px 14px;
  background: rgba(255, 255, 255, 0.04);
  border-bottom: 1px solid rgba(255, 255, 255, 0.06);
}

.nc-window-dots {
  display: flex;
  gap: 6px;
}

.nc-wdot {
  width: 10px;
  height: 10px;
  border-radius: 50%;
}

.nc-wdot-r { background: #ff5f57; }
.nc-wdot-y { background: #febc2e; }
.nc-wdot-g { background: #28c840; }

.nc-window-title {
  font-size: 0.6rem;
  color: rgba(255, 255, 255, 0.35);
  font-family: 'Fira Code', 'SF Mono', monospace !important;
  letter-spacing: 0.02em;
}

.nc-window-body {
  padding: 14px 18px;
  background: rgba(0, 0, 0, 0.3);
}

.nc-window-dark .nc-window-body {
  background: rgba(0, 0, 0, 0.5);
}

/* Strip inner code block styling */
.nc-window-body :deep(pre) {
  margin: 0 !important;
  padding: 0 !important;
  background: transparent !important;
  border: none !important;
  border-radius: 0 !important;
}
</style>
