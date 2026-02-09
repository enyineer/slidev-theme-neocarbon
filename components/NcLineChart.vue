<template>
  <div :style="{ height: height + 'px', width: '100%' }">
    <canvas ref="chartCanvas"></canvas>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { Chart, LineController, LineElement, PointElement, CategoryScale, LinearScale, Tooltip, Legend, Title, Filler } from 'chart.js'

Chart.register(LineController, LineElement, PointElement, CategoryScale, LinearScale, Tooltip, Legend, Title, Filler)

const props = defineProps({
  labels: { type: Array, required: true },
  datasets: { type: Array, default: null },
  data: { type: Array, default: null },
  colors: { type: Array, default: () => ['#E30613'] },
  title: { type: String, default: '' },
  yLabel: { type: String, default: '' },
  height: { type: Number, default: 240 },
  fill: { type: Boolean, default: true },
  smooth: { type: Boolean, default: true },
})

const chartCanvas = ref(null)

onMounted(() => {
  const ctx = chartCanvas.value.getContext('2d')
  const fontFamily = getComputedStyle(document.documentElement).getPropertyValue('--nc-font').trim() || "'Inter', sans-serif"

  // Support both simple (single dataset) and multi-dataset modes
  let datasets
  if (props.datasets) {
    datasets = props.datasets.map((ds, i) => {
      const color = ds.color || props.colors[i % props.colors.length]
      return {
        label: ds.label || '',
        data: ds.data,
        borderColor: color,
        backgroundColor: props.fill ? createGradient(ctx, color) : 'transparent',
        borderWidth: 2,
        pointBackgroundColor: color,
        pointBorderColor: '#0c0c0c',
        pointBorderWidth: 2,
        pointRadius: 3,
        pointHoverRadius: 6,
        tension: props.smooth ? 0.4 : 0,
        fill: props.fill,
      }
    })
  } else {
    const color = props.colors[0]
    datasets = [{
      data: props.data,
      borderColor: color,
      backgroundColor: props.fill ? createGradient(ctx, color) : 'transparent',
      borderWidth: 2,
      pointBackgroundColor: color,
      pointBorderColor: '#0c0c0c',
      pointBorderWidth: 2,
      pointRadius: 3,
      pointHoverRadius: 6,
      tension: props.smooth ? 0.4 : 0,
      fill: props.fill,
    }]
  }

  new Chart(ctx, {
    type: 'line',
    data: {
      labels: props.labels,
      datasets,
    },
    options: {
      responsive: true,
      maintainAspectRatio: false,
      plugins: {
        legend: {
          display: datasets.length > 1,
          labels: {
            color: 'rgba(255,255,255,0.6)',
            font: { size: 10, family: fontFamily },
            usePointStyle: true,
            pointStyleWidth: 8,
            padding: 12,
          },
        },
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

function createGradient(ctx, color) {
  const gradient = ctx.createLinearGradient(0, 0, 0, ctx.canvas.height)
  gradient.addColorStop(0, color + '30')
  gradient.addColorStop(1, color + '00')
  return gradient
}
</script>
