<template>
  <div :style="{ height: height + 'px', width: '100%' }">
    <canvas ref="chartCanvas"></canvas>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { Chart, DoughnutController, ArcElement, Tooltip, Legend, Title } from 'chart.js'

Chart.register(DoughnutController, ArcElement, Tooltip, Legend, Title)

const props = defineProps({
  labels: { type: Array, required: true },
  data: { type: Array, required: true },
  colors: { type: Array, default: () => ['#E30613', '#ff4444', '#ff6666', '#ff8888'] },
  title: { type: String, default: '' },
  height: { type: Number, default: 240 },
  doughnut: { type: Boolean, default: true },
})

const chartCanvas = ref(null)

onMounted(() => {
  const ctx = chartCanvas.value.getContext('2d')
  const fontFamily = getComputedStyle(document.documentElement).getPropertyValue('--nc-font').trim() || "'Inter', sans-serif"

  new Chart(ctx, {
    type: props.doughnut ? 'doughnut' : 'pie',
    data: {
      labels: props.labels,
      datasets: [{
        data: props.data,
        backgroundColor: props.colors,
        borderColor: 'var(--nc-bg, #0c0c0c)',
        borderWidth: 3,
        hoverOffset: 8,
      }],
    },
    options: {
      responsive: true,
      maintainAspectRatio: false,
      cutout: props.doughnut ? '58%' : 0,
      plugins: {
        legend: {
          position: 'right',
          labels: {
            color: 'rgba(255,255,255,0.6)',
            font: { size: 10, family: fontFamily },
            padding: 12,
            usePointStyle: true,
            pointStyleWidth: 8,
          },
        },
        title: {
          display: !!props.title,
          text: props.title,
          color: 'rgba(255,255,255,0.7)',
          font: { size: 12, family: fontFamily, weight: 'bold' },
          padding: { bottom: 8 },
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
    },
  })
})
</script>
