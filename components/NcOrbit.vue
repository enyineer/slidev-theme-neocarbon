<!--
  NcOrbit — Items orbiting around a central element with smooth rotation.
  Great for showing ecosystem, integrations, or related concepts.

  Usage:
    <NcOrbit 
      center="🧠" 
      centerLabel="Core"
      :items="['📊', '🔒', '🚀', '🌍', '⚡', '🔌']"
    />
-->
<script setup lang="ts">
import { computed } from 'vue'

const props = withDefaults(defineProps<{
  center?: string
  centerLabel?: string
  items: string[]
  size?: number
  speed?: number
}>(), {
  center: '⚛️',
  size: 260,
  speed: 30,
})

const orbitItems = computed(() => {
  const count = props.items.length
  return props.items.map((item, i) => ({
    item,
    angle: (360 / count) * i,
  }))
})
</script>

<template>
  <div class="nc-orbit-container" :style="{ width: size + 'px', height: size + 'px' }">
    <!-- Orbit ring -->
    <div class="nc-orbit-ring" :style="{ width: size + 'px', height: size + 'px' }" />

    <!-- Center -->
    <div class="nc-orbit-center">
      <span class="nc-orbit-center-icon">{{ center }}</span>
      <span v-if="centerLabel" class="nc-orbit-center-label">{{ centerLabel }}</span>
    </div>

    <!-- Orbiting items -->
    <div class="nc-orbit-track" :style="{ animationDuration: speed + 's' }">
      <div
        v-for="(orb, i) in orbitItems"
        :key="i"
        class="nc-orbit-item"
        :style="{
          transform: `rotate(${orb.angle}deg) translateX(${size / 2}px) rotate(-${orb.angle}deg)`,
          '--counter-angle': `-${orb.angle}deg`,
        }"
      >
        <div class="nc-orbit-item-inner" :style="{ animationDuration: speed + 's' }">
          {{ orb.item }}
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.nc-orbit-container {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
}

.nc-orbit-ring {
  position: absolute;
  border-radius: 50%;
  border: 1px dashed rgba(255, 255, 255, 0.08);
}

.nc-orbit-center {
  position: absolute;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 4px;
  z-index: 2;
}

.nc-orbit-center-icon {
  font-size: 2rem;
  width: 56px;
  height: 56px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: var(--nc-surface, #161616);
  border: 1px solid rgba(var(--nc-accent-rgb, 227, 6, 19), 0.3);
  border-radius: 50%;
  box-shadow: 0 0 30px rgba(var(--nc-accent-rgb, 227, 6, 19), 0.15);
}

.nc-orbit-center-label {
  font-size: 0.6rem;
  font-weight: 700;
  color: rgba(255, 255, 255, 0.5);
  text-transform: uppercase;
  letter-spacing: 0.05em;
}

.nc-orbit-track {
  position: absolute;
  width: 100%;
  height: 100%;
  animation: nc-orbit-spin linear infinite;
}

@keyframes nc-orbit-spin {
  from { transform: rotate(0deg); }
  to { transform: rotate(360deg); }
}

.nc-orbit-item {
  position: absolute;
  top: 50%;
  left: 50%;
  margin-top: -18px;
  margin-left: -18px;
  width: 36px;
  height: 36px;
}

.nc-orbit-item-inner {
  width: 36px;
  height: 36px;
  font-size: 1.1rem;
  display: flex;
  align-items: center;
  justify-content: center;
  background: var(--nc-surface, #161616);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 50%;
  animation: nc-orbit-counter-spin linear infinite;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.3);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.nc-orbit-item-inner:hover {
  transform: scale(1.3) !important;
  box-shadow: 0 0 20px rgba(var(--nc-accent-rgb, 227, 6, 19), 0.3);
  border-color: rgba(var(--nc-accent-rgb, 227, 6, 19), 0.3);
}

@keyframes nc-orbit-counter-spin {
  from { transform: rotate(0deg); }
  to { transform: rotate(-360deg); }
}
</style>
