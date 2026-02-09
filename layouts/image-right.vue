<!--
  NeοCarbon — Image Right Layout
  Content on the left, image/visual on the right.

  Usage:
    ---
    layout: image-right
    ---
    ::default::
    # Left Content
    Description text

    ::right::
    <img src="/screenshot.png" class="rounded-xl shadow-2xl" />
-->
<template>
  <div class="slidev-layout nc-image-right nc-custom-layout">
    <div class="nc-ir-content">
      <slot />
    </div>
    <div class="nc-ir-visual">
      <div class="nc-ir-frame">
        <slot name="right" />
      </div>
    </div>
  </div>
</template>

<style scoped>
.nc-image-right {
  display: flex !important;
  flex-direction: row !important;
  height: 100%;
  gap: 0;
}

.nc-ir-content {
  flex: 1;
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding: 2.5rem;
  padding-right: 1.5rem;
  animation: nc-ir-content-enter 0.7s cubic-bezier(0.16, 1, 0.3, 1) 0.1s both;
}

@keyframes nc-ir-content-enter {
  from { opacity: 0; transform: translateX(-20px); filter: blur(3px); }
  to { opacity: 1; transform: translateX(0); filter: blur(0); }
}

.nc-ir-content :deep(h1) {
  font-size: 1.6rem !important;
}

.nc-ir-visual {
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 2rem;
  position: relative;
}

/* Glow behind the visual */
.nc-ir-visual::before {
  content: '';
  position: absolute;
  width: 80%;
  height: 80%;
  background: radial-gradient(circle, rgba(var(--nc-accent-rgb, 227, 6, 19), 0.08) 0%, transparent 70%);
  border-radius: 50%;
  filter: blur(40px);
  pointer-events: none;
}

.nc-ir-frame {
  position: relative;
  z-index: 1;
  border-radius: 16px;
  overflow: hidden;
  border: 1px solid var(--nc-border);
  box-shadow:
    0 20px 60px rgba(0, 0, 0, 0.4),
    0 0 40px rgba(var(--nc-accent-rgb, 227, 6, 19), 0.06);
  animation: nc-frame-enter 0.8s cubic-bezier(0.16, 1, 0.3, 1) 0.2s both;
}

.nc-ir-frame :deep(img) {
  display: block;
  max-width: 100%;
  max-height: 100%;
  object-fit: contain;
}

@keyframes nc-frame-enter {
  from {
    opacity: 0;
    transform: translateX(30px) scale(0.95);
    filter: blur(6px);
  }
  to {
    opacity: 1;
    transform: translateX(0) scale(1);
    filter: blur(0);
  }
}
</style>
