<script setup lang="ts">
import { ref, onMounted } from 'vue'

const props = defineProps<{
  to: number
  prefix?: string
  suffix?: string
  duration?: number
  decimals?: number
  separator?: string
}>()

const displayed = ref('0')

function formatNumber(n: number): string {
  const fixed = n.toFixed(props.decimals ?? 0)
  const [intPart, decPart] = fixed.split('.')
  const sep = props.separator ?? '.'
  const formatted = intPart.replace(/\B(?=(\d{3})+(?!\d))/g, sep)
  return decPart !== undefined ? `${formatted},${decPart}` : formatted
}

function animate() {
  const duration = props.duration ?? 1800
  const start = performance.now()
  const target = props.to

  function tick(now: number) {
    const elapsed = now - start
    const progress = Math.min(elapsed / duration, 1)
    const eased = 1 - Math.pow(1 - progress, 4)
    const current = eased * target
    displayed.value = formatNumber(current)

    if (progress < 1) {
      requestAnimationFrame(tick)
    } else {
      displayed.value = formatNumber(target)
    }
  }

  requestAnimationFrame(tick)
}

onMounted(() => {
  setTimeout(animate, 400)
})
</script>

<template>
  <span class="nc-animated-counter">{{ prefix }}{{ displayed }}{{ suffix }}</span>
</template>

<style scoped>
.nc-animated-counter {
  font-variant-numeric: tabular-nums;
  display: inline-block;
}
</style>
