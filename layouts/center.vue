<!--
  NeοCarbon — Center Layout
  Simpler than cover, centers content both vertically and horizontally.

  Usage:
    ---
    layout: center
    ---
    # A statement slide
    One powerful message.

  Slots: default
-->
<template>
  <div class="slidev-layout nc-center">
    <div class="nc-center-inner">
      <slot />
    </div>
  </div>
</template>

<style scoped>
.nc-center {
  display: flex !important;
  align-items: center;
  justify-content: center;
  height: 100%;
  text-align: center;
  padding: 2.5rem !important;
}

.nc-center-inner {
  display: flex !important;
  flex-direction: column !important;
  align-items: center;
  justify-content: center;
}

.nc-center-inner :deep(h1) {
  font-size: 2rem !important;
  font-weight: 700 !important;
  letter-spacing: -0.01em;
}

.nc-center-inner :deep(p) {
  color: var(--nc-text-muted) !important;
  font-size: 0.85rem;
  max-width: 30rem;
  margin-top: 0.5rem;
}
</style>
