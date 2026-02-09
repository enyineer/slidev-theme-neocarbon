<!--
  NcGlow — Adds a pulsing accent glow behind any child content.

  Usage:
    <NcGlow>
      <h1>Wow!</h1>
    </NcGlow>
    <NcGlow color="#4ade80" :intensity="0.15" :size="300">
      <img src="/hero.png" />
    </NcGlow>
-->
<script setup lang="ts">
defineProps<{
  color?: string
  intensity?: number
  size?: number
}>()
</script>

<template>
  <div class="nc-glow-wrap">
    <div
      class="nc-glow-orb"
      :style="{
        background: `radial-gradient(circle, ${color || 'rgba(var(--nc-accent-rgb, 227, 6, 19), ' + (intensity || 0.12) + ')'} 0%, transparent 70%)`,
        width: (size || 250) + 'px',
        height: (size || 250) + 'px',
      }"
    />
    <div class="nc-glow-content">
      <slot />
    </div>
  </div>
</template>

<style scoped>
.nc-glow-wrap {
  position: relative;
  display: inline-flex;
  align-items: center;
  justify-content: center;
}

.nc-glow-orb {
  position: absolute;
  border-radius: 50%;
  filter: blur(50px);
  animation: nc-glow-pulse 4s ease-in-out infinite;
  pointer-events: none;
  z-index: 0;
}

@keyframes nc-glow-pulse {
  0%, 100% { transform: scale(1); opacity: 0.7; }
  50% { transform: scale(1.15); opacity: 1; }
}

.nc-glow-content {
  position: relative;
  z-index: 1;
}
</style>
