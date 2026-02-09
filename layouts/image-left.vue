<!--
  NeοCarbon — Image Left Layout
  Image/visual on the left, content on the right.

  Usage:
    ---
    layout: image-left
    ---
    ::left::
    <img src="/screenshot.png" class="rounded-xl shadow-2xl" />

    ::default::
    # Right Content
    Description text
-->
<template>
  <div class="slidev-layout nc-image-left nc-custom-layout">
    <div class="nc-il-visual">
      <div class="nc-il-frame">
        <slot name="left" />
      </div>
    </div>
    <div class="nc-il-content">
      <slot />
    </div>
  </div>
</template>

<style scoped>
.nc-image-left {
  display: flex !important;
  flex-direction: row !important;
  height: 100%;
  gap: 0;
}

.nc-il-content {
  flex: 1;
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding: 2.5rem;
  padding-left: 1.5rem;
  animation: nc-il-content-enter 0.7s cubic-bezier(0.16, 1, 0.3, 1) 0.2s both;
}

@keyframes nc-il-content-enter {
  from { opacity: 0; transform: translateX(20px); filter: blur(3px); }
  to { opacity: 1; transform: translateX(0); filter: blur(0); }
}

.nc-il-content :deep(h1) {
  font-size: 1.6rem !important;
}

.nc-il-visual {
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 2rem;
  position: relative;
}

.nc-il-visual::before {
  content: '';
  position: absolute;
  width: 80%;
  height: 80%;
  background: radial-gradient(circle, rgba(var(--nc-accent-rgb, 227, 6, 19), 0.08) 0%, transparent 70%);
  border-radius: 50%;
  filter: blur(40px);
  pointer-events: none;
}

.nc-il-frame {
  position: relative;
  z-index: 1;
  border-radius: 16px;
  overflow: hidden;
  border: 1px solid var(--nc-border);
  box-shadow:
    0 20px 60px rgba(0, 0, 0, 0.4),
    0 0 40px rgba(var(--nc-accent-rgb, 227, 6, 19), 0.06);
  animation: nc-frame-enter-left 0.8s cubic-bezier(0.16, 1, 0.3, 1) 0.1s both;
}

.nc-il-frame :deep(img) {
  display: block;
  max-width: 100%;
  max-height: 100%;
  object-fit: contain;
}

@keyframes nc-frame-enter-left {
  from {
    opacity: 0;
    transform: translateX(-30px) scale(0.95);
    filter: blur(6px);
  }
  to {
    opacity: 1;
    transform: translateX(0) scale(1);
    filter: blur(0);
  }
}
</style>
