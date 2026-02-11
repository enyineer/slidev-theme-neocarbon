<!--
  NcFlipCard — 3D card that flips on hover to reveal a back side.

  Usage:
    <NcFlipCard>
      <template #front>
        <h2>🔒</h2>
        <p>Hover to reveal</p>
      </template>
      <template #back>
        <h2>🎉</h2>
        <p>Surprise!</p>
      </template>
    </NcFlipCard>
-->
<script setup lang="ts">
defineProps<{
  width?: string;
  height?: string;
}>();
</script>

<template>
  <div
    class="nc-flip"
    :style="{ width: width || '180px', height: height || '200px' }"
  >
    <div class="nc-flip-inner">
      <div class="nc-flip-front">
        <slot name="front" />
      </div>
      <div class="nc-flip-back">
        <slot name="back" />
      </div>
    </div>
  </div>
</template>

<style scoped>
.nc-flip {
  perspective: 800px;
  cursor: pointer;
}

.nc-flip-inner {
  position: relative;
  width: 100%;
  height: 100%;
  transition: transform 0.6s cubic-bezier(0.4, 0, 0.2, 1);
  transform-style: preserve-3d;
}

.nc-flip:hover .nc-flip-inner {
  transform: rotateY(180deg);
}

.nc-flip-front,
.nc-flip-back {
  position: absolute;
  inset: 0;
  backface-visibility: hidden;
  -webkit-backface-visibility: hidden;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 16px;
  border-radius: 14px;
  text-align: center;
  border: 1px solid rgba(255, 255, 255, 0.08);
}

.nc-flip-front {
  background: var(--nc-surface, #161616);
}

.nc-flip-back {
  background: #1a0608;
  border-color: rgba(var(--nc-accent-rgb, 227, 6, 19), 0.3);
  transform: rotateY(180deg);
}

.nc-flip-front :deep(h2),
.nc-flip-back :deep(h2) {
  font-size: 1.8rem !important;
  margin-bottom: 6px;
}

.nc-flip-front :deep(p),
.nc-flip-back :deep(p) {
  font-size: 0.65rem !important;
  color: var(--nc-text-muted) !important;
}

.nc-flip-back :deep(p) {
  color: rgba(255, 255, 255, 0.8) !important;
}
</style>
