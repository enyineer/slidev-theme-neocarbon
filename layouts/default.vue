<!--
  NeοCarbon — Default Layout
  Standard content slide with a label + heading area and content body.
  Stagger entrance is handled by global-top.vue via the .nc-active class.

  Usage:
    ---
    layout: default
    ---
    # Slide Title
    Your content here…

  Slots: default
-->
<template>
  <div class="slidev-layout nc-default nc-custom-layout">
    <div class="nc-default-inner">
      <slot />
    </div>
  </div>
</template>

<style scoped>
.nc-default {
  height: 100%;
  padding: 2.5rem !important;
}

.nc-default-inner {
  display: flex !important;
  flex-direction: column !important;
  height: 100%;
}

.nc-default-inner :deep(h1) {
  font-size: 1.6rem !important;
}

/*
 * Stagger entrance — controlled by .nc-active class from global-top.vue.
 * Targets up to 3 levels deep so cards inside grid columns each get
 * their own explicit opacity transition (fixes Firefox compositing order
 * issue with backdrop-filter / animation pseudo-elements).
 */
.nc-default-inner :deep(> *),
.nc-default-inner :deep(> * > *),
.nc-default-inner :deep(> * > * > *) {
  opacity: 0;
  transform: translateY(12px);
  transition: opacity 0.5s cubic-bezier(0.16, 1, 0.3, 1),
              transform 0.5s cubic-bezier(0.16, 1, 0.3, 1) !important;
}

.nc-active .nc-default-inner :deep(> *),
.nc-active .nc-default-inner :deep(> * > *),
.nc-active .nc-default-inner :deep(> * > * > *) {
  opacity: 1;
  transform: translateY(0);
}

/* Stagger delays — level 1: direct children */
.nc-active .nc-default-inner :deep(> *:nth-child(1)) { transition-delay: 0.05s; }
.nc-active .nc-default-inner :deep(> *:nth-child(2)) { transition-delay: 0.12s; }
.nc-active .nc-default-inner :deep(> *:nth-child(3)) { transition-delay: 0.19s; }
.nc-active .nc-default-inner :deep(> *:nth-child(4)) { transition-delay: 0.26s; }
.nc-active .nc-default-inner :deep(> *:nth-child(5)) { transition-delay: 0.33s; }
.nc-active .nc-default-inner :deep(> *:nth-child(6)) { transition-delay: 0.40s; }
.nc-active .nc-default-inner :deep(> *:nth-child(7)) { transition-delay: 0.47s; }
.nc-active .nc-default-inner :deep(> *:nth-child(8)) { transition-delay: 0.54s; }

/* Stagger delays — level 2: grid columns etc */
.nc-active .nc-default-inner :deep(> * > *:nth-child(1)) { transition-delay: 0.10s; }
.nc-active .nc-default-inner :deep(> * > *:nth-child(2)) { transition-delay: 0.16s; }

/* Stagger delays — level 3: cards inside grid columns */
.nc-active .nc-default-inner :deep(> * > * > *:nth-child(1)) { transition-delay: 0.14s; }
.nc-active .nc-default-inner :deep(> * > * > *:nth-child(2)) { transition-delay: 0.22s; }
.nc-active .nc-default-inner :deep(> * > * > *:nth-child(3)) { transition-delay: 0.30s; }
.nc-active .nc-default-inner :deep(> * > * > *:nth-child(4)) { transition-delay: 0.38s; }
.nc-active .nc-default-inner :deep(> * > * > *:nth-child(5)) { transition-delay: 0.46s; }
.nc-active .nc-default-inner :deep(> * > * > *:nth-child(6)) { transition-delay: 0.54s; }
.nc-active .nc-default-inner :deep(> * > * > *:nth-child(7)) { transition-delay: 0.62s; }
.nc-active .nc-default-inner :deep(> * > * > *:nth-child(8)) { transition-delay: 0.70s; }
</style>
