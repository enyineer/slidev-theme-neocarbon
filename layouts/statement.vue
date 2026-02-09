<!--
  NeοCarbon — Statement Layout
  A dramatic full-screen layout for a single bold message.
  The heading gets an animated gradient text effect.

  Usage:
    ---
    layout: statement
    ---
    # We need to act now.
-->
<template>
  <div class="slidev-layout nc-statement nc-custom-layout">
    <div class="nc-statement-bg" />
    <div class="nc-statement-inner">
      <slot />
    </div>
  </div>
</template>

<style scoped>
.nc-statement {
  display: flex !important;
  flex-direction: column !important;
  align-items: center !important;
  justify-content: center !important;
  height: 100%;
  text-align: center;
  padding: 3rem !important;
  position: relative;
  overflow: hidden;
}

.nc-statement-bg {
  position: absolute;
  inset: 0;
  background: radial-gradient(
    ellipse 60% 50% at 50% 50%,
    rgba(var(--nc-accent-rgb, 227, 6, 19), 0.05) 0%,
    transparent 100%
  );
  animation: nc-statement-breathe 6s ease-in-out infinite;
}

@keyframes nc-statement-breathe {
  0%, 100% { opacity: 0.5; transform: scale(1); }
  50% { opacity: 1; transform: scale(1.05); }
}

.nc-statement-inner {
  position: relative;
  z-index: 1;
  max-width: 40rem;
  animation: nc-stmt-enter 0.8s cubic-bezier(0.16, 1, 0.3, 1) 0.2s both;
}

@keyframes nc-stmt-enter {
  from { opacity: 0; transform: translateY(20px); filter: blur(6px); }
  to { opacity: 1; transform: translateY(0); filter: blur(0); }
}

.nc-statement-inner :deep(h1) {
  font-size: 2.8rem !important;
  font-weight: 800 !important;
  letter-spacing: -0.03em;
  line-height: 1.15 !important;
  color: white !important;
  -webkit-text-fill-color: white !important;
  text-shadow: 0 0 60px rgba(var(--nc-accent-rgb, 227, 6, 19), 0.3);
}

.nc-statement-inner :deep(p) {
  color: var(--nc-text-muted) !important;
  font-size: 0.9rem !important;
  margin-top: 1.5rem !important;
  max-width: 28rem;
  margin-left: auto;
  margin-right: auto;
}
</style>
