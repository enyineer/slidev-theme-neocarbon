<!--
  NeοCarbon — Two Columns Layout
  Split content into left and right columns.

  Usage:
    ---
    layout: two-cols
    ---
    ::left::
    Left side content

    ::right::
    Right side content

  Slots: left, right
-->
<template>
  <div class="slidev-layout nc-two-cols nc-custom-layout">
    <div class="nc-two-cols-inner">
      <div class="nc-col nc-col-left">
        <slot name="left" />
      </div>
      <div class="nc-col nc-col-right">
        <slot name="right" />
      </div>
    </div>
  </div>
</template>

<style scoped>
.nc-two-cols {
  height: 100%;
  padding: 2.5rem !important;
}

.nc-two-cols-inner {
  display: flex !important;
  flex-direction: row !important;
  gap: 1.5rem;
  height: 100%;
}

.nc-col {
  flex: 1;
  display: flex;
  flex-direction: column;
}

/* Staggered entry animation for columns */
.nc-col-left {
  animation: nc-col-enter 0.7s cubic-bezier(0.16, 1, 0.3, 1) 0.1s both;
}

.nc-col-right {
  animation: nc-col-enter 0.7s cubic-bezier(0.16, 1, 0.3, 1) 0.25s both;
}

@keyframes nc-col-enter {
  from {
    opacity: 0;
    transform: translateY(18px);
    filter: blur(4px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
    filter: blur(0);
  }
}

.nc-col :deep(h1) {
  font-size: 1.6rem !important;
}
</style>
