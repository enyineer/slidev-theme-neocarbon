<!--
  NeοCarbon — Quote Layout
  A cinematic full-screen quote slide with oversized quotation marks,
  a glow accent, and an optional attribution line.

  Usage:
    ---
    layout: quote
    ---
    The best way to predict the future is to invent it.

    — Alan Kay
-->
<template>
  <div class="slidev-layout nc-quote nc-custom-layout">
    <div class="nc-quote-glow" />
    <div class="nc-quote-mark nc-quote-open">"</div>
    <div class="nc-quote-body">
      <slot />
    </div>
    <div class="nc-quote-mark nc-quote-close">"</div>
  </div>
</template>

<style scoped>
.nc-quote {
  display: flex !important;
  flex-direction: column !important;
  align-items: center !important;
  justify-content: center !important;
  height: 100%;
  text-align: center;
  padding: 3rem 4rem !important;
  position: relative;
  overflow: hidden;
}

.nc-quote-glow {
  position: absolute;
  width: 500px;
  height: 500px;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background: radial-gradient(circle, rgba(var(--nc-accent-rgb, 227, 6, 19), 0.06) 0%, transparent 70%);
  pointer-events: none;
  animation: nc-quote-pulse 6s ease-in-out infinite;
}

@keyframes nc-quote-pulse {
  0%, 100% { transform: translate(-50%, -50%) scale(1); opacity: 0.6; }
  50% { transform: translate(-50%, -50%) scale(1.15); opacity: 1; }
}

.nc-quote-mark {
  font-size: 6rem;
  line-height: 1;
  color: var(--nc-accent);
  opacity: 0.2;
  font-family: Georgia, 'Times New Roman', serif !important;
  user-select: none;
  position: relative;
  z-index: 1;
}

.nc-quote-open {
  align-self: flex-start;
  margin-bottom: -2rem;
  animation: nc-q-enter 0.7s cubic-bezier(0.16, 1, 0.3, 1) 0.1s both;
}

.nc-quote-close {
  align-self: flex-end;
  margin-top: -2rem;
  animation: nc-q-enter 0.7s cubic-bezier(0.16, 1, 0.3, 1) 0.4s both;
}

.nc-quote-body {
  position: relative;
  z-index: 1;
  max-width: 36rem;
  animation: nc-q-enter 0.7s cubic-bezier(0.16, 1, 0.3, 1) 0.2s both;
}

.nc-quote-body :deep(p:first-child) {
  font-size: 1.3rem !important;
  font-weight: 500 !important;
  color: white !important;
  line-height: 1.6 !important;
  font-style: italic;
}

/* Attribution line (last paragraph starting with — or -) */
.nc-quote-body :deep(p:last-child) {
  font-size: 0.8rem !important;
  color: var(--nc-text-muted) !important;
  margin-top: 1.5rem !important;
  font-style: normal;
  font-weight: 600;
  letter-spacing: 0.02em;
}

@keyframes nc-q-enter {
  from { opacity: 0; transform: translateY(18px); filter: blur(4px); }
  to { opacity: 1; transform: translateY(0); filter: blur(0); }
}
</style>
