<!--
  NeοCarbon — Fact Layout
  A single powerful statistic or fact, massively centered with a glow ring.

  Usage:
    ---
    layout: fact
    ---
    # 47.5M €
    Estimated savings over 3 years
-->
<template>
  <div class="slidev-layout nc-fact nc-custom-layout">
    <div class="nc-fact-ring" />
    <div class="nc-fact-inner">
      <slot />
    </div>
  </div>
</template>

<style scoped>
.nc-fact {
  display: flex !important;
  flex-direction: column !important;
  align-items: center !important;
  justify-content: center !important;
  height: 100%;
  text-align: center;
  padding: 2.5rem !important;
  position: relative;
  overflow: hidden;
}

/* Glowing ring behind the fact */
.nc-fact-ring {
  position: absolute;
  width: 320px;
  height: 320px;
  border-radius: 50%;
  border: 2px solid rgba(var(--nc-accent-rgb, 227, 6, 19), 0.15);
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%) scale(0.8);
  opacity: 0;
  animation: nc-ring-enter 1.2s cubic-bezier(0.16, 1, 0.3, 1) 0.3s forwards;
  box-shadow:
    0 0 60px rgba(var(--nc-accent-rgb, 227, 6, 19), 0.08),
    inset 0 0 60px rgba(var(--nc-accent-rgb, 227, 6, 19), 0.04);
}

.nc-fact-ring::after {
  content: '';
  position: absolute;
  inset: -20px;
  border-radius: 50%;
  border: 1px solid rgba(var(--nc-accent-rgb, 227, 6, 19), 0.06);
  animation: nc-ring-pulse 4s ease-in-out infinite;
}

@keyframes nc-ring-enter {
  to {
    opacity: 1;
    transform: translate(-50%, -50%) scale(1);
  }
}

@keyframes nc-ring-pulse {
  0%, 100% { transform: scale(1); opacity: 1; }
  50% { transform: scale(1.08); opacity: 0.6; }
}

.nc-fact-inner {
  position: relative;
  z-index: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  animation: nc-fact-fade 0.8s cubic-bezier(0.16, 1, 0.3, 1) 0.4s both;
}

@keyframes nc-fact-fade {
  from { opacity: 0; transform: scale(0.9); filter: blur(6px); }
  to { opacity: 1; transform: scale(1); filter: blur(0); }
}

.nc-fact-inner :deep(h1) {
  font-size: 4rem !important;
  font-weight: 900 !important;
  letter-spacing: -0.03em;
  line-height: 1 !important;
  color: white !important;
  -webkit-text-fill-color: white !important;
  text-shadow: 0 0 40px rgba(var(--nc-accent-rgb, 227, 6, 19), 0.4);
}

.nc-fact-inner :deep(p) {
  font-size: 0.9rem !important;
  color: var(--nc-text-muted) !important;
  margin-top: 1rem !important;
  max-width: 24rem;
}
</style>
