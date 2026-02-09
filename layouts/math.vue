<!--
  NeοCarbon — Math Layout
  Optimized for KaTeX formulas. Provides a centered formula area
  with a subtle chalkboard feel and elegant typography.

  Usage:
    ---
    layout: math
    ---
    # Euler's Identity

    $$
    e^{i\pi} + 1 = 0
    $$

    The most beautiful equation in mathematics.
-->
<template>
  <div class="slidev-layout nc-math nc-custom-layout">
    <div class="nc-math-glow" />
    <div class="nc-math-inner">
      <slot />
    </div>
  </div>
</template>

<style scoped>
.nc-math {
  display: flex !important;
  flex-direction: column !important;
  align-items: center !important;
  justify-content: center !important;
  height: 100%;
  text-align: center;
  padding: 2.5rem 3rem !important;
  position: relative;
  overflow: hidden;
}

.nc-math-glow {
  position: absolute;
  width: 600px;
  height: 300px;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background: radial-gradient(
    ellipse,
    rgba(var(--nc-accent-rgb, 227, 6, 19), 0.04) 0%,
    transparent 70%
  );
  animation: nc-math-breathe 8s ease-in-out infinite;
  pointer-events: none;
}

@keyframes nc-math-breathe {
  0%, 100% { opacity: 0.5; transform: translate(-50%, -50%) scale(1); }
  50% { opacity: 1; transform: translate(-50%, -50%) scale(1.1); }
}

.nc-math-inner {
  position: relative;
  z-index: 1;
  max-width: 42rem;
  animation: nc-math-enter 0.8s cubic-bezier(0.16, 1, 0.3, 1) 0.2s both;
}

@keyframes nc-math-enter {
  from { opacity: 0; transform: translateY(16px); filter: blur(4px); }
  to { opacity: 1; transform: translateY(0); filter: blur(0); }
}

.nc-math-inner :deep(h1) {
  font-size: 1.6rem !important;
  margin-bottom: 1.5rem !important;
}

/* KaTeX display math styling */
.nc-math-inner :deep(.katex-display) {
  margin: 1.5rem 0 !important;
  padding: 1.5rem 2rem;
  background: rgba(255, 255, 255, 0.02);
  border: 1px solid rgba(255, 255, 255, 0.06);
  border-radius: 14px;
  position: relative;
  overflow: hidden;
}

/* Shimmer on the formula block */
.nc-math-inner :deep(.katex-display)::after {
  content: '';
  position: absolute;
  top: -50%;
  left: -50%;
  width: 200%;
  height: 200%;
  background: linear-gradient(115deg,
    transparent 40%,
    rgba(255, 255, 255, 0.02) 45%,
    rgba(255, 255, 255, 0.04) 50%,
    rgba(255, 255, 255, 0.02) 55%,
    transparent 60%
  );
  animation: nc-shimmer 8s ease-in-out infinite;
  pointer-events: none;
}

@keyframes nc-shimmer {
  0%, 100% { transform: translateX(-100%); }
  50% { transform: translateX(100%); }
}

.nc-math-inner :deep(.katex) {
  font-size: 1.6rem !important;
  color: white !important;
}

.nc-math-inner :deep(.katex .base) {
  color: white;
}

.nc-math-inner :deep(p) {
  color: var(--nc-text-muted) !important;
  font-size: 0.8rem !important;
  max-width: 30rem;
  margin: 0 auto;
}

/* Inline math */
.nc-math-inner :deep(.katex-inline) {
  color: var(--nc-accent) !important;
}
</style>
