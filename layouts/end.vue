<!--
  NeοCarbon — End Layout
  Closing/CTA slide with centered layout, large heading, and call-to-action area.

  Usage:
    ---
    layout: end
    ---
    # Thank You
    Questions & Discussion

  Slots: default
-->
<template>
  <div class="slidev-layout nc-end">
    <div class="nc-end-inner">
      <slot />
    </div>
  </div>
</template>

<style scoped>
.nc-end {
  display: flex !important;
  align-items: center;
  justify-content: center;
  height: 100%;
  text-align: center;
  padding: 2.5rem !important;
}

.nc-end-inner {
  display: flex !important;
  flex-direction: column !important;
  align-items: center;
  justify-content: center;
}

.nc-end-inner :deep(h1) {
  font-size: 2.2rem !important;
  font-weight: 700 !important;
  letter-spacing: -0.02em;
}

.nc-end-inner :deep(p) {
  color: var(--nc-text-muted) !important;
  font-size: 0.8rem;
  max-width: 28rem;
  line-height: 1.6;
}

.nc-end-inner :deep(img) {
  height: 2.25rem;
  width: auto;
  margin-bottom: 1.25rem;
  opacity: 0.9;
}

/* Final muted text (e.g. "Questions & Discussions") */
.nc-end-inner :deep(p:last-of-type) {
  color: rgba(255, 255, 255, 0.2) !important;
  font-size: 0.65rem;
  margin-top: 2rem;
}
</style>
