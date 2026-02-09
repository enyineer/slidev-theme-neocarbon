<!--
  NeοCarbon — Code Layout
  Optimized for Monaco editor / code blocks. Wraps code in a
  macOS-style window frame with title bar dots. The heading
  renders naturally above the window.

  Usage:
    ---
    layout: code
    ---
    # API Handler

    ```ts
    export async function handler(req: Request) {
      const data = await req.json()
      return Response.json({ ok: true })
    }
    ```
-->
<template>
  <div class="slidev-layout nc-code nc-custom-layout">
    <div class="nc-code-inner">
      <slot />
    </div>
  </div>
</template>

<style scoped>
.nc-code {
  display: flex !important;
  flex-direction: column !important;
  height: 100%;
  padding: 2rem 2.5rem !important;
}

.nc-code-inner {
  flex: 1;
  display: flex;
  flex-direction: column;
  min-height: 0;
  animation: nc-code-enter 0.6s cubic-bezier(0.16, 1, 0.3, 1) 0.1s both;
}

@keyframes nc-code-enter {
  from { opacity: 0; transform: translateY(10px); }
  to { opacity: 1; transform: translateY(0); }
}

.nc-code-inner :deep(h1) {
  font-size: 1.3rem !important;
  margin-bottom: 0.75rem !important;
  flex-shrink: 0;
}

/* === Window chrome on the outermost code wrapper only === */
.nc-code-inner :deep(.slidev-code-wrapper) {
  border-radius: 14px !important;
  border: 1px solid rgba(255, 255, 255, 0.08) !important;
  box-shadow: 0 20px 60px rgba(0, 0, 0, 0.4), 0 0 1px rgba(255, 255, 255, 0.1) !important;
  overflow: hidden !important;
  position: relative !important;
  padding-top: 38px !important;
  background: rgba(0, 0, 0, 0.3) !important;
  flex: 1;
  min-height: 0;
}

/* Title bar with traffic light dots */
.nc-code-inner :deep(.slidev-code-wrapper)::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 38px;
  border-bottom: 1px solid rgba(255, 255, 255, 0.06);
  z-index: 10;
  pointer-events: none;
  background-image:
    radial-gradient(circle 5px at 20px 19px, #ff5f57 5px, transparent 5px),
    radial-gradient(circle 5px at 36px 19px, #febc2e 5px, transparent 5px),
    radial-gradient(circle 5px at 52px 19px, #28c840 5px, transparent 5px);
  background-repeat: no-repeat;
  background-color: rgba(255, 255, 255, 0.04);
}

/* Strip ALL styling from the inner pre — the wrapper handles it */
.nc-code-inner :deep(.slidev-code-wrapper pre),
.nc-code-inner :deep(.slidev-code-wrapper .shiki) {
  margin: 0 !important;
  padding: 14px 18px !important;
  border: none !important;
  border-radius: 0 !important;
  background: transparent !important;
  box-shadow: none !important;
}

.nc-code-inner :deep(.slidev-code-wrapper pre)::before {
  display: none !important;
}

.nc-code-inner :deep(.slidev-code-wrapper pre code) {
  font-family: 'Fira Code', 'SF Mono', 'Cascadia Code', monospace !important;
  font-size: 0.78rem !important;
  line-height: 1.7 !important;
}

/* Monaco editor container */
.nc-code-inner :deep(.slidev-monaco) {
  border-radius: 14px !important;
  overflow: hidden !important;
  border: 1px solid rgba(255, 255, 255, 0.08) !important;
}
</style>
