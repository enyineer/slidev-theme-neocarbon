<!--
  NeοCarbon — Cover Layout
  Full-screen centered hero slide with optional logo.

  Usage:
    ---
    layout: cover
    ---
    # Your Title
    Subtitle text

  Slots: default
-->
<template>
  <div class="slidev-layout nc-cover">
    <div class="nc-cover-inner">
      <slot />
    </div>
  </div>
</template>

<style scoped>
.nc-cover {
  display: flex !important;
  align-items: center;
  justify-content: center;
  height: 100%;
  text-align: center;
  padding: 2.5rem !important;
}

.nc-cover-inner {
  display: flex !important;
  flex-direction: column !important;
  align-items: center;
  justify-content: center;
  max-width: 42rem;
}

.nc-cover-inner :deep(h1) {
  font-size: 2.4rem !important;
  font-weight: 700 !important;
  letter-spacing: -0.02em;
  line-height: 1.2 !important;
}

.nc-cover-inner :deep(p) {
  color: var(--nc-text-muted) !important;
  font-size: 0.85rem !important;
  line-height: 1.6;
  max-width: 32rem;
}

.nc-cover-inner :deep(img) {
  height: 2.25rem;
  width: auto;
  margin-bottom: 1.5rem;
  opacity: 0.9;
}
</style>
