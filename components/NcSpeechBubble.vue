<!--
  NcSpeechBubble — Chat-style message bubbles for testimonials or conversations.
  Uses v-click-compatible visibility so it works with Slidev's navigation.

  Usage:
    <NcSpeechBubble from="Alice" avatar="👩" side="left" :delay="0">
      This product changed everything for us!
    </NcSpeechBubble>
    <NcSpeechBubble from="You" avatar="🤖" side="right" accent :delay="1">
      Thank you! We're glad to hear that.
    </NcSpeechBubble>
-->
<script setup lang="ts">
import { ref, onMounted, onUnmounted, watch } from 'vue'

const props = withDefaults(defineProps<{
  from?: string
  avatar?: string
  side?: 'left' | 'right'
  accent?: boolean
  delay?: number
}>(), {
  delay: 0,
})

const root = ref<HTMLElement | null>(null)
const visible = ref(false)
let observer: IntersectionObserver | null = null
let showTimer: ReturnType<typeof setTimeout> | null = null
let wasVisible = false

function show() {
  const delayMs = 300 + (props.delay * 300)
  showTimer = setTimeout(() => { visible.value = true }, delayMs)
}

function hide() {
  if (showTimer) clearTimeout(showTimer)
  visible.value = false
  wasVisible = false
}

onMounted(() => {
  if (!root.value) return
  observer = new IntersectionObserver(
    (entries) => {
      const entry = entries[0]
      if (entry.isIntersecting && !wasVisible) {
        wasVisible = true
        show()
      } else if (!entry.isIntersecting) {
        hide()
      }
    },
    { threshold: 0.1 }
  )
  // Delay observe to avoid first-frame flash
  requestAnimationFrame(() => {
    requestAnimationFrame(() => {
      if (root.value) observer?.observe(root.value)
    })
  })
})

onUnmounted(() => {
  if (showTimer) clearTimeout(showTimer)
  observer?.disconnect()
})
</script>

<template>
  <div ref="root" :class="['nc-bubble-wrap', `nc-bubble-${side || 'left'}`, { 'nc-bubble-show': visible }]">
    <div v-if="avatar" class="nc-bubble-avatar">{{ avatar }}</div>
    <div :class="['nc-bubble', { 'nc-bubble-accent': accent }]">
      <p v-if="from" class="nc-bubble-from">{{ from }}</p>
      <div class="nc-bubble-body"><slot /></div>
    </div>
  </div>
</template>

<style scoped>
.nc-bubble-wrap {
  display: flex;
  align-items: flex-end;
  gap: 8px;
  max-width: 75%;
  opacity: 0;
  transform: translateY(12px) scale(0.92);
  transition: opacity 0.5s cubic-bezier(0.16, 1, 0.3, 1),
              transform 0.5s cubic-bezier(0.34, 1.56, 0.64, 1);
  /* Override the base stagger animation so we control visibility ourselves */
  animation: none !important;
}

.nc-bubble-show {
  opacity: 1;
  transform: translateY(0) scale(1);
}

.nc-bubble-left {
  align-self: flex-start;
}

.nc-bubble-right {
  align-self: flex-end;
  flex-direction: row-reverse;
  margin-left: auto;
}

.nc-bubble-avatar {
  width: 28px;
  height: 28px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1rem;
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(255, 255, 255, 0.08);
  flex-shrink: 0;
}

.nc-bubble {
  padding: 8px 14px;
  border-radius: 16px;
  background: var(--nc-surface, #161616);
  border: 1px solid rgba(255, 255, 255, 0.06);
  position: relative;
}

.nc-bubble-left .nc-bubble {
  border-bottom-left-radius: 4px;
}

.nc-bubble-right .nc-bubble {
  border-bottom-right-radius: 4px;
}

.nc-bubble-accent {
  background: rgba(var(--nc-accent-rgb, 227, 6, 19), 0.12) !important;
  border-color: rgba(var(--nc-accent-rgb, 227, 6, 19), 0.2) !important;
}

.nc-bubble-from {
  font-size: 0.55rem !important;
  font-weight: 700 !important;
  color: rgba(255, 255, 255, 0.35) !important;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  margin-bottom: 3px;
}

.nc-bubble-body {
  font-size: 0.72rem !important;
  color: rgba(255, 255, 255, 0.75) !important;
  line-height: 1.5;
}

.nc-bubble-accent .nc-bubble-body {
  color: white !important;
}
</style>
