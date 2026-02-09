<!--
  NeοCarbon — Diagram Layout
  Optimized for Mermaid diagrams with dark theme overrides.
  Content (title/description) on the left, diagram on the right.

  Usage:
    ---
    layout: diagram
    ---
    ::left::
    # System Architecture
    High-level overview of the platform

    ::right::
    ```mermaid
    graph TD
      A[Client] --> B[API]
      B --> C[Database]
    ```
-->
<template>
  <div class="slidev-layout nc-diagram nc-custom-layout">
    <div class="nc-diagram-content">
      <slot name="left" />
    </div>
    <div class="nc-diagram-visual">
      <div class="nc-diagram-frame">
        <slot name="right" />
      </div>
    </div>
  </div>
</template>

<style scoped>
.nc-diagram {
  display: flex !important;
  flex-direction: row !important;
  height: 100%;
  gap: 0;
}

.nc-diagram-content {
  width: 35%;
  flex-shrink: 0;
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding: 2.5rem;
  animation: nc-diag-left 0.7s cubic-bezier(0.16, 1, 0.3, 1) 0.1s both;
}

@keyframes nc-diag-left {
  from { opacity: 0; transform: translateX(-16px); }
  to { opacity: 1; transform: translateX(0); }
}

.nc-diagram-content :deep(h1) {
  font-size: 1.4rem !important;
}

.nc-diagram-visual {
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 1.5rem 2rem;
  position: relative;
  overflow: hidden;
}

/* Subtle grid behind the diagram */
.nc-diagram-visual::before {
  content: '';
  position: absolute;
  inset: 0;
  background-image:
    linear-gradient(rgba(255, 255, 255, 0.015) 1px, transparent 1px),
    linear-gradient(90deg, rgba(255, 255, 255, 0.015) 1px, transparent 1px);
  background-size: 40px 40px;
  mask-image: radial-gradient(ellipse 80% 70% at 50% 50%, black 20%, transparent 80%);
  -webkit-mask-image: radial-gradient(ellipse 80% 70% at 50% 50%, black 20%, transparent 80%);
}

.nc-diagram-frame {
  position: relative;
  z-index: 1;
  width: 100%;
  animation: nc-diag-right 0.8s cubic-bezier(0.16, 1, 0.3, 1) 0.25s both;
}

@keyframes nc-diag-right {
  from { opacity: 0; transform: scale(0.94); filter: blur(4px); }
  to { opacity: 1; transform: scale(1); filter: blur(0); }
}

/* === Mermaid dark theme overrides === */
.nc-diagram-frame :deep(.mermaid) {
  display: flex;
  justify-content: center;
}

.nc-diagram-frame :deep(.mermaid svg) {
  max-width: 100%;
  max-height: 400px;
}

.nc-diagram-frame :deep(.mermaid .node rect),
.nc-diagram-frame :deep(.mermaid .node circle),
.nc-diagram-frame :deep(.mermaid .node polygon) {
  fill: var(--nc-surface, #161616) !important;
  stroke: rgba(var(--nc-accent-rgb, 227, 6, 19), 0.4) !important;
  stroke-width: 1.5px !important;
}

.nc-diagram-frame :deep(.mermaid .nodeLabel),
.nc-diagram-frame :deep(.mermaid .label) {
  color: white !important;
  fill: white !important;
  font-family: var(--nc-font) !important;
  font-size: 12px !important;
}

.nc-diagram-frame :deep(.mermaid .edgePath path) {
  stroke: rgba(var(--nc-accent-rgb, 227, 6, 19), 0.5) !important;
  stroke-width: 1.5px !important;
}

.nc-diagram-frame :deep(.mermaid .arrowheadPath) {
  fill: rgba(var(--nc-accent-rgb, 227, 6, 19), 0.6) !important;
}

.nc-diagram-frame :deep(.mermaid .edgeLabel) {
  background-color: var(--nc-bg, #0c0c0c) !important;
  color: rgba(255, 255, 255, 0.6) !important;
  font-size: 10px !important;
}
</style>
