<!--
  NeοCarbon — Split Heading Layout
  Magazine-style: big heading pinned on the left, scrollable content on the right.

  Usage:
    ---
    layout: split-heading
    ---
    ::left::
    # Big Heading

    ::right::
    Content body...
-->
<template>
  <div class="slidev-layout nc-split-heading nc-custom-layout">
    <div class="nc-sh-heading">
      <div class="nc-sh-accent" />
      <slot name="left" />
    </div>
    <div class="nc-sh-content">
      <slot name="right" />
    </div>
  </div>
</template>

<style scoped>
.nc-split-heading {
  display: flex !important;
  flex-direction: row !important;
  height: 100%;
}

.nc-sh-heading {
  width: 38%;
  flex-shrink: 0;
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding: 2.5rem;
  position: relative;
  animation: nc-sh-left 0.7s cubic-bezier(0.16, 1, 0.3, 1) 0.1s both;
}

@keyframes nc-sh-left {
  from { opacity: 0; transform: translateX(-20px); }
  to { opacity: 1; transform: translateX(0); }
}

.nc-sh-accent {
  position: absolute;
  right: 0;
  top: 15%;
  bottom: 15%;
  width: 2px;
  background: linear-gradient(
    180deg,
    transparent,
    rgba(var(--nc-accent-rgb, 227, 6, 19), 0.3) 30%,
    rgba(var(--nc-accent-rgb, 227, 6, 19), 0.3) 70%,
    transparent
  );
}

.nc-sh-heading :deep(h1) {
  font-size: 2rem !important;
  font-weight: 800 !important;
  letter-spacing: -0.02em;
  line-height: 1.2 !important;
}

.nc-sh-heading :deep(p) {
  color: var(--nc-text-muted) !important;
  font-size: 0.8rem !important;
  margin-top: 0.5rem;
}

.nc-sh-content {
  flex: 1;
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding: 2.5rem;
  animation: nc-sh-right 0.7s cubic-bezier(0.16, 1, 0.3, 1) 0.25s both;
}

@keyframes nc-sh-right {
  from { opacity: 0; transform: translateX(20px); filter: blur(3px); }
  to { opacity: 1; transform: translateX(0); filter: blur(0); }
}
</style>
