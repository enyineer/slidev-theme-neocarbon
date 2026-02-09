<!--
  NeοCarbon — Comparison Layout
  Side-by-side comparison with distinct visual treatment.
  Perfect for "before vs after", "current vs future", "option A vs B".

  Usage:
    ---
    layout: comparison
    ---
    ::left::
    ❌ **Before**
    Old way of doing things

    ::right::
    ✅ **After**
    New way of doing things

  Slots: left, right
-->
<template>
  <div class="slidev-layout nc-comparison nc-custom-layout">
    <slot />
    <div class="nc-comparison-inner">
      <div class="nc-compare-panel nc-compare-left">
        <slot name="left" />
      </div>
      <div class="nc-compare-divider" />
      <div class="nc-compare-panel nc-compare-right">
        <slot name="right" />
      </div>
    </div>
  </div>
</template>

<style scoped>
.nc-comparison {
  height: 100%;
  padding: 2.5rem !important;
  display: flex !important;
  flex-direction: column !important;
}

.nc-comparison-inner {
  display: flex !important;
  flex-direction: row !important;
  gap: 0;
  flex: 1;
  animation: nc-comp-enter 0.7s cubic-bezier(0.16, 1, 0.3, 1) 0.15s both;
}

@keyframes nc-comp-enter {
  from { opacity: 0; transform: translateY(14px); filter: blur(3px); }
  to { opacity: 1; transform: translateY(0); filter: blur(0); }
}

.nc-compare-panel {
  flex: 1;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  padding: 1rem;
  border-radius: 14px;
}

.nc-compare-panel :deep(> *) {
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  flex: 1;
}

.nc-compare-left {
  background: var(--nc-surface);
  border: 1px solid var(--nc-border);
}

.nc-compare-right {
  background: linear-gradient(135deg, rgba(var(--nc-success-rgb), 0.06), rgba(var(--nc-success-rgb), 0.02));
  border: 1px solid rgba(var(--nc-success-rgb), 0.15);
}

.nc-compare-divider {
  width: 1px;
  margin: 1rem 0.75rem;
  background: linear-gradient(
    180deg,
    transparent,
    rgba(255, 255, 255, 0.1) 30%,
    rgba(255, 255, 255, 0.1) 70%,
    transparent
  );
}

.nc-compare-panel :deep(h1),
.nc-compare-panel :deep(h3) {
  font-size: 1.1rem !important;
}

.nc-compare-panel :deep(strong) {
  color: white !important;
}
</style>
