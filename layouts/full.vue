<!--
  NeοCarbon — Full Layout
  Edge-to-edge content, no padding. Ideal for full-bleed images,
  embedded demos, or completely custom compositions.

  Usage:
    ---
    layout: full
    ---
    <img src="/hero.jpg" class="w-full h-full object-cover" />
-->
<template>
  <div class="slidev-layout nc-full">
    <slot />
  </div>
</template>

<style scoped>
.nc-full {
  height: 100%;
  padding: 0 !important;
  overflow: hidden;
  position: relative;
}

.nc-full :deep(> *) {
  animation: none !important;
}
</style>
