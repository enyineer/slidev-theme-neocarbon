<!--
  NcTerminal — Terminal/console display with typed-on content.

  Usage:
    <NcTerminal title="~/project">
      <span class="nc-term-prompt">$</span> npm run build
      <span class="nc-term-success">✓ Build complete in 1.2s</span>
    </NcTerminal>
-->
<script setup lang="ts">
defineProps<{
  title?: string
}>()
</script>

<template>
  <div class="nc-terminal">
    <div class="nc-terminal-bar">
      <div class="nc-terminal-dots">
        <span class="nc-tdot nc-tdot-r" />
        <span class="nc-tdot nc-tdot-y" />
        <span class="nc-tdot nc-tdot-g" />
      </div>
      <span class="nc-terminal-title">{{ title || 'Terminal' }}</span>
    </div>
    <div class="nc-terminal-body">
      <slot />
      <span class="nc-terminal-cursor" />
    </div>
  </div>
</template>

<style scoped>
.nc-terminal {
  border-radius: 14px;
  overflow: hidden;
  border: 1px solid rgba(255, 255, 255, 0.08);
  box-shadow: 0 16px 50px rgba(0, 0, 0, 0.4);
  animation: nc-term-enter 0.6s cubic-bezier(0.16, 1, 0.3, 1) both;
}

@keyframes nc-term-enter {
  from { opacity: 0; transform: translateY(10px) scale(0.97); }
  to { opacity: 1; transform: translateY(0) scale(1); }
}

.nc-terminal-bar {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 10px 14px;
  background: rgba(255, 255, 255, 0.04);
  border-bottom: 1px solid rgba(255, 255, 255, 0.06);
}

.nc-terminal-dots {
  display: flex;
  gap: 6px;
}

.nc-tdot {
  width: 10px;
  height: 10px;
  border-radius: 50%;
}

.nc-tdot-r { background: #ff5f57; }
.nc-tdot-y { background: #febc2e; }
.nc-tdot-g { background: #28c840; }

.nc-terminal-title {
  font-size: 0.6rem;
  color: rgba(255, 255, 255, 0.3);
  font-family: 'Fira Code', 'SF Mono', monospace !important;
}

.nc-terminal-body {
  background: #0a0a0a;
  padding: 14px 18px;
  font-family: 'Fira Code', 'SF Mono', 'Cascadia Code', monospace !important;
  font-size: 0.72rem;
  line-height: 1.8;
  color: rgba(255, 255, 255, 0.7);
  white-space: pre-wrap;
  position: relative;
}

.nc-terminal-cursor {
  display: inline-block;
  width: 8px;
  height: 14px;
  background: var(--nc-accent, #E30613);
  margin-left: 2px;
  animation: nc-cursor-blink 1s step-end infinite;
  vertical-align: text-bottom;
  opacity: 0.8;
}

@keyframes nc-cursor-blink {
  0%, 100% { opacity: 0.8; }
  50% { opacity: 0; }
}
</style>

<style>
/* Global styles for child elements */
.nc-term-prompt {
  color: var(--nc-accent, #E30613) !important;
  font-weight: 700;
  margin-right: 6px;
}

.nc-term-success {
  color: var(--nc-success, #4ade80) !important;
}

.nc-term-error {
  color: var(--nc-danger, #ea580c) !important;
}

.nc-term-warn {
  color: var(--nc-warning, #fbbf24) !important;
}

.nc-term-dim {
  color: rgba(255, 255, 255, 0.3) !important;
}

.nc-term-info {
  color: var(--nc-info, #60a5fa) !important;
}
</style>
