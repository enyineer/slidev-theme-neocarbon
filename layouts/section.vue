<!--
  NeοCarbon — Section Layout
  A chapter divider / section title slide.
  Large centered heading with optional description.

  Usage:
    ---
    layout: section
    ---
    # Chapter 3
    The interesting part

  Slots: default
-->
<template>
  <div class="slidev-layout nc-section">
    <div class="nc-section-inner">
      <slot />
    </div>
  </div>
</template>

<style scoped>
.nc-section {
  display: flex !important;
  align-items: center;
  justify-content: center;
  height: 100%;
  text-align: center;
  padding: 3rem !important;
}

.nc-section-inner {
  display: flex !important;
  flex-direction: column !important;
  align-items: center;
  justify-content: center;
}

.nc-section-inner :deep(h1) {
  font-size: 2rem !important;
  font-weight: 700 !important;
  letter-spacing: -0.02em;
  margin-bottom: 0.5rem !important;
}

.nc-section-inner :deep(p) {
  color: var(--nc-text-muted) !important;
  font-size: 0.9rem !important;
  max-width: 30rem;
}

/* Accent underline below h1 */
.nc-section-inner :deep(h1)::after {
  content: '';
  display: block;
  width: 3rem;
  height: 3px;
  background: var(--nc-accent);
  margin: 0.75rem auto 0;
  border-radius: 2px;
  box-shadow: 0 0 12px rgba(var(--nc-accent-rgb), 0.5);
}
</style>
