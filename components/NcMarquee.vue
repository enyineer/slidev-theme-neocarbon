<!--
  NcMarquee — Infinitely scrolling horizontal marquee for logos, tech stack, etc.

  Usage:
    <NcMarquee :items="['React', 'Vue', 'TypeScript', 'Rust', 'Go']" />
    <NcMarquee :items="['AWS', 'GCP', 'Azure']" :speed="40" reverse />
-->
<script setup lang="ts">
defineProps<{
  items: string[]
  speed?: number
  reverse?: boolean
}>()
</script>

<template>
  <div class="nc-marquee-wrap">
    <div
      :class="['nc-marquee-track', { 'nc-marquee-reverse': reverse }]"
      :style="{ '--speed': (speed || 30) + 's' }"
    >
      <span v-for="(item, i) in [...items, ...items]" :key="i" class="nc-marquee-item">
        {{ item }}
      </span>
    </div>
  </div>
</template>

<style scoped>
.nc-marquee-wrap {
  overflow: hidden;
  mask-image: linear-gradient(90deg, transparent, black 10%, black 90%, transparent);
  -webkit-mask-image: linear-gradient(90deg, transparent, black 10%, black 90%, transparent);
  padding: 8px 0;
}

.nc-marquee-track {
  display: flex;
  gap: 2rem;
  width: max-content;
  animation: nc-marquee-scroll var(--speed) linear infinite;
}

.nc-marquee-reverse {
  animation-direction: reverse;
}

@keyframes nc-marquee-scroll {
  0% { transform: translateX(0); }
  100% { transform: translateX(-50%); }
}

.nc-marquee-item {
  font-size: 0.7rem;
  font-weight: 700;
  color: rgba(255, 255, 255, 0.3);
  text-transform: uppercase;
  letter-spacing: 0.08em;
  white-space: nowrap;
  padding: 6px 16px;
  background: rgba(255, 255, 255, 0.03);
  border: 1px solid rgba(255, 255, 255, 0.06);
  border-radius: 100px;
  transition: all 0.3s ease;
}

.nc-marquee-item:hover {
  color: white;
  border-color: rgba(var(--nc-accent-rgb, 227, 6, 19), 0.3);
  background: rgba(var(--nc-accent-rgb, 227, 6, 19), 0.08);
}
</style>
