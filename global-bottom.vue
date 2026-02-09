<template>
  <div class="nc-bg-layer">
    <!-- Ambient gradient orbs -->
    <div class="nc-orb nc-orb-1" />
    <div class="nc-orb nc-orb-2" />
    <div class="nc-orb nc-orb-3" />

    <!-- Floating particles -->
    <div class="nc-particles">
      <div v-for="i in 12" :key="i" class="nc-particle" :style="particleStyle(i)" />
    </div>

    <!-- Subtle grid overlay -->
    <div class="nc-grid-overlay" />

    <!-- Noise grain texture -->
    <div class="nc-noise" />

    <!-- Top accent glow -->
    <div class="nc-top-glow" />

    <!-- Vignette for depth -->
    <div class="nc-vignette" />
  </div>
</template>

<script setup>
function particleStyle(i) {
  const seed = i * 7.3
  const left = ((seed * 13.7) % 100)
  const top = ((seed * 17.1) % 100)
  const size = 1.5 + (seed % 3)
  const duration = 15 + (seed % 20)
  const delay = (seed % 8)
  const opacity = 0.08 + (seed % 5) * 0.02
  return {
    left: `${left}%`,
    top: `${top}%`,
    width: `${size}px`,
    height: `${size}px`,
    '--duration': `${duration}s`,
    '--delay': `${delay}s`,
    '--opacity': opacity,
  }
}
</script>

<style scoped>
.nc-bg-layer {
  position: absolute;
  inset: 0;
  overflow: hidden;
  pointer-events: none;
  z-index: 0;
}

/* === GRADIENT ORBS === */
.nc-orb {
  position: absolute;
  border-radius: 50%;
  filter: blur(100px);
  opacity: 0;
  will-change: transform, opacity;
}

.nc-orb-1 {
  width: 700px;
  height: 700px;
  background: radial-gradient(circle, rgba(var(--nc-accent-rgb, 227, 6, 19), 0.12) 0%, rgba(var(--nc-accent-rgb, 227, 6, 19), 0.04) 40%, transparent 70%);
  top: -20%;
  right: -10%;
  animation: nc-orb-drift-1 24s ease-in-out infinite, nc-orb-fade-in 3s ease-out 0.3s forwards;
}

.nc-orb-2 {
  width: 600px;
  height: 600px;
  background: radial-gradient(circle, rgba(var(--nc-accent-rgb, 227, 6, 19), 0.07) 0%, rgba(var(--nc-accent-rgb, 227, 6, 19), 0.03) 50%, transparent 70%);
  bottom: -20%;
  left: -15%;
  animation: nc-orb-drift-2 30s ease-in-out infinite, nc-orb-fade-in 3s ease-out 0.8s forwards;
}

.nc-orb-3 {
  width: 450px;
  height: 450px;
  background: radial-gradient(circle, rgba(255, 100, 50, 0.05) 0%, rgba(var(--nc-accent-rgb, 227, 6, 19), 0.02) 40%, transparent 70%);
  top: 30%;
  left: 40%;
  animation: nc-orb-drift-3 22s ease-in-out infinite, nc-orb-fade-in 3s ease-out 1.2s forwards;
}

@keyframes nc-orb-fade-in {
  to { opacity: 1; }
}

@keyframes nc-orb-drift-1 {
  0%, 100% { transform: translate(0, 0) scale(1); }
  25% { transform: translate(-50px, 40px) scale(1.06); }
  50% { transform: translate(-25px, -30px) scale(0.94); }
  75% { transform: translate(35px, 15px) scale(1.03); }
}

@keyframes nc-orb-drift-2 {
  0%, 100% { transform: translate(0, 0) scale(1); }
  33% { transform: translate(60px, -35px) scale(1.08); }
  66% { transform: translate(-40px, 25px) scale(0.92); }
}

@keyframes nc-orb-drift-3 {
  0%, 100% { transform: translate(0, 0) scale(1); }
  20% { transform: translate(-35px, -45px) scale(1.12); }
  40% { transform: translate(25px, -15px) scale(0.94); }
  60% { transform: translate(-15px, 35px) scale(1.06); }
  80% { transform: translate(45px, 20px) scale(0.97); }
}

/* === FLOATING PARTICLES === */
.nc-particles {
  position: absolute;
  inset: 0;
}

.nc-particle {
  position: absolute;
  border-radius: 50%;
  background: rgba(var(--nc-accent-rgb, 227, 6, 19), 0.6);
  box-shadow: 0 0 6px 1px rgba(var(--nc-accent-rgb, 227, 6, 19), 0.3);
  opacity: 0;
  animation: nc-particle-float var(--duration) ease-in-out var(--delay) infinite;
}

@keyframes nc-particle-float {
  0%, 100% {
    transform: translateY(0) translateX(0);
    opacity: 0;
  }
  10% {
    opacity: var(--opacity);
  }
  50% {
    transform: translateY(-30px) translateX(15px);
    opacity: var(--opacity);
  }
  90% {
    opacity: var(--opacity);
  }
}

/* === SUBTLE GRID === */
.nc-grid-overlay {
  position: absolute;
  inset: 0;
  background-image:
    linear-gradient(rgba(255, 255, 255, 0.018) 1px, transparent 1px),
    linear-gradient(90deg, rgba(255, 255, 255, 0.018) 1px, transparent 1px);
  background-size: 80px 80px;
  mask-image: radial-gradient(ellipse 80% 70% at 50% 50%, black 20%, transparent 80%);
  -webkit-mask-image: radial-gradient(ellipse 80% 70% at 50% 50%, black 20%, transparent 80%);
  opacity: 0;
  animation: nc-fade-in 4s ease-out 1s forwards;
}

/* === NOISE GRAIN === */
.nc-noise {
  position: absolute;
  inset: -50%;
  width: 200%;
  height: 200%;
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.85' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.025'/%3E%3C/svg%3E");
  opacity: 0.5;
  pointer-events: none;
  animation: nc-noise-shift 0.4s steps(4) infinite;
}

@keyframes nc-noise-shift {
  0% { transform: translate(0, 0); }
  25% { transform: translate(-1px, 1px); }
  50% { transform: translate(1px, -1px); }
  75% { transform: translate(-1px, -1px); }
  100% { transform: translate(0, 0); }
}

/* === TOP ACCENT GLOW === */
.nc-top-glow {
  position: absolute;
  top: -2px;
  left: 0;
  right: 0;
  height: 120px;
  background: linear-gradient(180deg,
    rgba(var(--nc-accent-rgb, 227, 6, 19), 0.08) 0%,
    rgba(var(--nc-accent-rgb, 227, 6, 19), 0.02) 40%,
    transparent 100%
  );
  opacity: 0;
  animation: nc-fade-in 2s ease-out 0.5s forwards;
}

/* === VIGNETTE === */
.nc-vignette {
  position: absolute;
  inset: 0;
  background: radial-gradient(ellipse 75% 65% at 50% 45%, transparent 35%, rgba(0, 0, 0, 0.5) 100%);
  pointer-events: none;
}

@keyframes nc-fade-in {
  to { opacity: 1; }
}
</style>
