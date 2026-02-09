<!--
  NeοCarbon — Metrics Layout
  A slide layout optimized for displaying 3-4 KPI metric cards in a row
  with an optional content area below.

  Usage:
    ---
    layout: metrics
    ---
    ::metrics::
    <div class="nc-metric" style="border-top: 2px solid var(--nc-accent)">
      <p style="font-size: 1.1rem; font-weight: 900; color: white">7.7M €</p>
      <p style="font-size: 0.6rem; color: var(--nc-text-muted)">Total Cost</p>
    </div>
    <!-- more metrics... -->

    ::default::
    Additional content below the metrics

  Slots: metrics, default
-->
<template>
  <div class="slidev-layout nc-metrics">
    <div class="nc-metrics-inner">
      <div class="nc-metrics-row">
        <slot name="metrics" />
      </div>
      <div class="nc-metrics-body">
        <slot />
      </div>
    </div>
  </div>
</template>

<style scoped>
.nc-metrics {
  height: 100%;
  padding: 2.5rem !important;
}

.nc-metrics-inner {
  display: flex !important;
  flex-direction: column !important;
  height: 100%;
}

.nc-metrics-row {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
  gap: 0.75rem;
  margin-bottom: 1rem;
}

.nc-metrics-body {
  flex: 1;
  display: flex;
  flex-direction: column;
}

.nc-metrics-row :deep(h1) {
  font-size: 1.6rem !important;
  grid-column: 1 / -1;
}
</style>
