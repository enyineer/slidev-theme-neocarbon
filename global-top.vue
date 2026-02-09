<!--
  NeoCarbon — Global Top Layer
  Accent line at top + global stagger animation controller.
  Uses MutationObserver to detect new slides and IntersectionObserver to
  toggle .nc-stagger-active / .nc-active for replay on every navigation.
-->
<script setup lang="ts">
import { onMounted, onUnmounted } from 'vue'

let mutationObs: MutationObserver | null = null
let intersectionObs: IntersectionObserver | null = null
const observed = new WeakSet<Element>()

function setupIntersectionObserver() {
  intersectionObs = new IntersectionObserver(
    (entries) => {
      for (const entry of entries) {
        const el = entry.target as HTMLElement
        if (entry.isIntersecting) {
          // Remove first to reset transition state, then re-add after a frame
          el.classList.remove('nc-stagger-active', 'nc-active')
          requestAnimationFrame(() => {
            requestAnimationFrame(() => {
              el.classList.add('nc-stagger-active', 'nc-active')
            })
          })
        } else {
          el.classList.remove('nc-stagger-active', 'nc-active')
        }
      }
    },
    { threshold: 0.15 }
  )
}

function observeLayouts() {
  const layouts = document.querySelectorAll('.slidev-layout')
  layouts.forEach((el) => {
    if (!observed.has(el) && intersectionObs) {
      intersectionObs.observe(el)
      observed.add(el)
    }
  })
}

onMounted(() => {
  setupIntersectionObserver()

  // Initial scan
  requestAnimationFrame(() => {
    observeLayouts()
  })

  // Watch for new slides being added to the DOM
  mutationObs = new MutationObserver(() => {
    observeLayouts()
  })
  mutationObs.observe(document.body, { childList: true, subtree: true })
})

onUnmounted(() => {
  mutationObs?.disconnect()
  intersectionObs?.disconnect()
})
</script>

<template>
  <div class="nc-top-accent">
    <div class="nc-accent-line" />
  </div>
</template>

<style scoped>
.nc-top-accent {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  z-index: 10;
  pointer-events: none;
}

.nc-accent-line {
  height: 2px;
  background: linear-gradient(
    90deg,
    transparent 0%,
    rgba(var(--nc-accent-rgb, 227, 6, 19), 0.3) 15%,
    rgba(var(--nc-accent-rgb, 227, 6, 19), 0.8) 50%,
    rgba(var(--nc-accent-rgb, 227, 6, 19), 0.3) 85%,
    transparent 100%
  );
  opacity: 0;
  animation: nc-line-enter 1.2s cubic-bezier(0.16, 1, 0.3, 1) 0.2s forwards;
}

@keyframes nc-line-enter {
  from {
    opacity: 0;
    transform: scaleX(0);
  }
  to {
    opacity: 1;
    transform: scaleX(1);
  }
}
</style>
