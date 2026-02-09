<template>
  <div :style="{ height: height + 'px', width: '100%' }">
    <canvas ref="chartCanvas"></canvas>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { Chart, BarController, BarElement, CategoryScale, LinearScale, Tooltip, Legend, Title } from 'chart.js'

Chart.register(BarController, BarElement, CategoryScale, LinearScale, Tooltip, Legend, Title)

const props = defineProps({
  labels: { type: Array, required: true },
  data: { type: Array, required: true },
  colors: { type: Array, default: () => ['var(--nc-accent, #E30613)'] },
  title: { type: String, default: '' },
  yLabel: { type: String, default: '' },
  height: { type: Number, default: 240 },
  horizontal: { type: Boolean, default: false },
})

const chartCanvas = ref(null)

onMounted(() => {
  const ctx = chartCanvas.value.getContext('2d')
  const bgColors = props.labels.map((_, i) => props.colors[i % props.colors.length])
  const fontFamily = getComputedStyle(document.documentElement).getPropertyValue('--nc-font').trim() || "'Inter', sans-serif"

  new Chart(ctx, {
    type: 'bar',
    data: {
      labels: props.labels,
      datasets: [{
        data: props.data,
        backgroundColor: bgColors.map(c => c + 'CC'),
        borderColor: bgColors,
        borderWidth: 1,
        borderRadius: 6,
        barPercentage: 0.55,
      }],
    },
    options: {
      indexAxis: props.horizontal ? 'y' : 'x',
      responsive: true,
      maintainAspectRatio: false,
      plugins: {
        legend: { display: false },
        title: {
          display: !!props.title,
          text: props.title,
          color: 'rgba(255,255,255,0.7)',
          font: { size: 12, family: fontFamily, weight: 'bold' },
          padding: { bottom: 12 },
        },
        tooltip: {
          backgroundColor: '#1a1a1a',
          titleColor: 'white',
          bodyColor: 'rgba(255,255,255,0.7)',
          borderColor: 'rgba(255,255,255,0.1)',
          borderWidth: 1,
          cornerRadius: 8,
          padding: 10,
          titleFont: { family: fontFamily, weight: 'bold' },
          bodyFont: { family: fontFamily },
        },
      },
      scales: {
        x: {
          grid: { color: 'rgba(255,255,255,0.04)', drawBorder: false },
          ticks: { color: 'rgba(255,255,255,0.4)', font: { size: 10, family: fontFamily } },
          border: { display: false },
        },
        y: {
          grid: { color: 'rgba(255,255,255,0.04)', drawBorder: false },
          ticks: { color: 'rgba(255,255,255,0.4)', font: { size: 10, family: fontFamily } },
          border: { display: false },
          title: {
            display: !!props.yLabel,
            text: props.yLabel,
            color: 'rgba(255,255,255,0.3)',
            font: { size: 10, family: fontFamily },
          },
        },
      },
    },
  })
})
</script>
