<!--
  NcTypewriter — Text that types itself character by character.
  Re-triggers animation each time the slide is navigated to.

  Usage:
    <NcTypewriter text="Hello, World!" :speed="60" cursor />
    <NcTypewriter :lines="['First line', 'Second line', 'Third line']" :speed="40" />
-->
<script setup lang="ts">
import { ref, onMounted, onUnmounted, nextTick } from 'vue'

const props = withDefaults(defineProps<{
  text?: string
  lines?: string[]
  speed?: number
  delay?: number
  cursor?: boolean
  loop?: boolean
}>(), {
  speed: 50,
  delay: 300,
  cursor: true,
  loop: false,
})

const root = ref<HTMLElement | null>(null)
const displayed = ref('')
const isTyping = ref(false)
let stopped = false
let timers: ReturnType<typeof setTimeout>[] = []
let observer: IntersectionObserver | null = null

function wait(ms: number): Promise<void> {
  return new Promise((resolve) => {
    const t = setTimeout(resolve, ms)
    timers.push(t)
  })
}

async function typeText(fullText: string) {
  isTyping.value = true
  for (let i = 0; i < fullText.length; i++) {
    if (stopped) return
    displayed.value += fullText.charAt(i)
    await wait(props.speed)
  }
  isTyping.value = false
}

async function run() {
  await nextTick()
  await wait(props.delay)

  const allLines = props.lines || [props.text || '']

  for (let l = 0; l < allLines.length; l++) {
    if (stopped) return
    if (l > 0) displayed.value += '\n'
    await typeText(allLines[l])
    if (l < allLines.length - 1) {
      await wait(300)
    }
  }

  if (props.loop && !stopped) {
    await wait(2000)
    displayed.value = ''
    await wait(500)
    run()
  }
}

function reset() {
  stopped = true
  timers.forEach(clearTimeout)
  timers = []
  displayed.value = ''
  isTyping.value = false
}

function start() {
  reset()
  stopped = false
  run()
}

onMounted(() => {
  if (!root.value) return
  // Double-RAF so browser paints initial state before we observe
  requestAnimationFrame(() => {
    requestAnimationFrame(() => {
      if (!root.value) return
      observer = new IntersectionObserver(
        (entries) => {
          for (const entry of entries) {
            if (entry.isIntersecting) {
              start()
            } else {
              reset()
            }
          }
        },
        { threshold: 0.1 }
      )
      observer.observe(root.value)
    })
  })
})

onUnmounted(() => {
  reset()
  observer?.disconnect()
})
</script>

<template>
  <span ref="root" class="nc-typewriter">
    <span class="nc-tw-text" v-html="displayed.replace(/\n/g, '<br/>')" />
    <span v-if="cursor" :class="['nc-tw-cursor', { 'nc-tw-blink': !isTyping }]">▎</span>
  </span>
</template>

<style scoped>
.nc-typewriter {
  display: inline;
}

.nc-tw-text {
  white-space: pre-wrap;
}

.nc-tw-cursor {
  color: var(--nc-accent, #E30613);
  font-weight: 300;
  animation: none;
  margin-left: 1px;
}

.nc-tw-blink {
  animation: nc-tw-blink 1s step-end infinite;
}

@keyframes nc-tw-blink {
  0%, 100% { opacity: 1; }
  50% { opacity: 0; }
}
</style>
