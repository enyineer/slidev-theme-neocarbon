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
  <div class="slidev-layout nc-two-cols">
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
  gap: 1.5rem;
  height: 100%;
}

.nc-col {
  flex: 1;
  display: flex;
  flex-direction: column;
}

.nc-col :deep(h1) {
  font-size: 1.6rem !important;
}
</style>
