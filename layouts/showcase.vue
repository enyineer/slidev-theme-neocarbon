<!--
  NeοCarbon — Showcase Layout
  A grid of visual items (screenshots, features, team members).
  Supports 2-4 columns with staggered entrance animations.

  Usage:
    ---
    layout: showcase
    ---
    # Feature Highlights

    <div class="nc-showcase-grid">
      <div class="nc-showcase-item">
        <img src="/screen1.png" />
        <p>Dashboard</p>
      </div>
      <div class="nc-showcase-item">
        <img src="/screen2.png" />
        <p>Analytics</p>
      </div>
    </div>
-->
<template>
  <div class="slidev-layout nc-showcase nc-custom-layout">
    <div class="nc-showcase-inner">
      <slot />
    </div>
  </div>
</template>

<style scoped>
.nc-showcase {
  display: flex !important;
  flex-direction: column !important;
  height: 100%;
  padding: 2rem 2.5rem !important;
}

.nc-showcase-inner {
  flex: 1;
  display: flex;
  flex-direction: column;
  animation: nc-show-enter 0.6s cubic-bezier(0.16, 1, 0.3, 1) 0.1s both;
}

@keyframes nc-show-enter {
  from { opacity: 0; transform: translateY(12px); }
  to { opacity: 1; transform: translateY(0); }
}

.nc-showcase-inner :deep(h1) {
  font-size: 1.4rem !important;
  margin-bottom: 0.75rem !important;
  flex-shrink: 0;
}

/* Grid defined globally in base.css */
</style>
