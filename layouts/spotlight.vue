<!--
  NeοCarbon — Spotlight Layout
  Dark stage with a spotlight effect illuminating centered content.
  Perfect for dramatic reveals and key announcements.

  Usage:
    ---
    layout: spotlight
    ---
    # We just raised $50M
    Series B led by Sequoia Capital
-->
<template>
  <div class="slidev-layout nc-spotlight nc-custom-layout">
    <!-- Light beam (triangle) -->
    <div class="nc-spot-beam" />
    <!-- Light pool (where the beam hits) -->
    <div class="nc-spot-pool" />
    <!-- Radial halo around content -->
    <div class="nc-spot-halo" />
    <div class="nc-spot-content">
      <slot />
    </div>
  </div>
</template>

<style scoped>
.nc-spotlight {
  display: flex !important;
  flex-direction: column !important;
  align-items: center !important;
  justify-content: center !important;
  height: 100%;
  text-align: center;
  padding: 2.5rem !important;
  position: relative;
  overflow: hidden;
  background: #020202 !important;
}

/* Triangular light beam from top center */
.nc-spot-beam {
  position: absolute;
  top: -20px;
  left: 50%;
  transform: translateX(-50%);
  width: 0;
  height: 0;
  border-left: 120px solid transparent;
  border-right: 120px solid transparent;
  border-top: 500px solid rgba(255, 255, 255, 0.035);
  filter: blur(30px);
  animation: nc-spot-sway 8s ease-in-out infinite;
  pointer-events: none;
  z-index: 0;
}

@keyframes nc-spot-sway {
  0%, 100% { transform: translateX(-50%) rotate(-1deg); }
  50% { transform: translateX(-50%) rotate(1deg); }
}

/* Bright pool of light in the center */
.nc-spot-pool {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 500px;
  height: 500px;
  border-radius: 50%;
  background: radial-gradient(
    circle,
    rgba(255, 255, 255, 0.06) 0%,
    rgba(255, 255, 255, 0.025) 30%,
    rgba(255, 255, 255, 0.008) 50%,
    transparent 70%
  );
  pointer-events: none;
  z-index: 0;
}

/* Soft warm halo behind/around the content */
.nc-spot-halo {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 300px;
  height: 200px;
  border-radius: 50%;
  background: radial-gradient(
    ellipse,
    rgba(255, 255, 255, 0.04) 0%,
    transparent 70%
  );
  animation: nc-spot-breathe 5s ease-in-out infinite;
  pointer-events: none;
  z-index: 0;
}

@keyframes nc-spot-breathe {
  0%, 100% { opacity: 0.8; transform: translate(-50%, -50%) scale(1); }
  50% { opacity: 1; transform: translate(-50%, -50%) scale(1.1); }
}

.nc-spot-content {
  position: relative;
  z-index: 1;
  max-width: 36rem;
  animation: nc-spot-reveal 1s cubic-bezier(0.16, 1, 0.3, 1) 0.3s both;
}

@keyframes nc-spot-reveal {
  from { opacity: 0; transform: translateY(20px) scale(0.95); filter: blur(6px); }
  to { opacity: 1; transform: translateY(0) scale(1); filter: blur(0); }
}

.nc-spot-content :deep(h1) {
  font-size: 2.2rem !important;
  font-weight: 800 !important;
  letter-spacing: -0.03em;
  line-height: 1.1 !important;
  text-shadow:
    0 0 60px rgba(255, 255, 255, 0.15),
    0 0 120px rgba(255, 255, 255, 0.05);
}

.nc-spot-content :deep(p) {
  color: rgba(255, 255, 255, 0.45) !important;
  font-size: 0.85rem !important;
  margin-top: 0.75rem;
}
</style>
