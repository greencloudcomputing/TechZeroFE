<template>
  <div class="card" style="position: relative; width: 100%">
    <Chart type="line" :data="chartData" :height="300" :options="chartOptions" />
  </div>
</template>

<script setup lang="ts">
import { format } from 'date-fns'
const props = defineProps<{
  data: {
    carbonIntensity: string
    // cost: number
    // electricityUsed: string
    // memoryUsed: string
    timestamp: string
  }[]
}>()

import Chart from 'primevue/chart'

import { ref, onMounted } from 'vue'

onMounted(() => {
  chartData.value = setChartData()
  chartOptions.value = setChartOptions()
})

const chartData = ref()
const chartOptions = ref()

const setChartData = () => {
  const documentStyle = getComputedStyle(document.documentElement)

  return {
    labels: props.data.map((element) => format(new Date(element.timestamp), 'dd/MM HH:mm')),
    datasets: [
      //   {
      //     label: 'Electricity used',
      //     data: props.data.map((element) => element.electricityUsed),
      //     fill: false,
      //     borderColor: documentStyle.getPropertyValue('--p-cyan-500'),
      //     tension: 0.4
      //   },
      {
        label: 'Carbon intensity',
        data: props.data.map((element) => element.carbonIntensity),
        fill: false,
        borderColor: documentStyle.getPropertyValue('--p-gray-500'),
        tension: 0.4
      }
      //   {
      //     label: 'Cost',
      //     data: props.data.map((element) => element.cost),
      //     fill: false,
      //     borderColor: documentStyle.getPropertyValue('--p-cyan-500'),
      //     tension: 0.4
      //   },
      //   {
      //     label: 'Memory used',
      //     data: props.data.map((element) => element.memoryUsed),
      //     fill: false,
      //     borderColor: documentStyle.getPropertyValue('--p-cyan-500'),
      //     tension: 0.4
      //   }
    ]
  }
}
const setChartOptions = () => {
  const documentStyle = getComputedStyle(document.documentElement)
  const textColor = documentStyle.getPropertyValue('--p-text-color')
  const textColorSecondary = documentStyle.getPropertyValue('--p-text-muted-color')
  const surfaceBorder = documentStyle.getPropertyValue('--p-content-border-color')

  return {
    maintainAspectRatio: false,
    aspectRatio: 0.6,
    plugins: {
      legend: {
        labels: {
          color: textColor
        }
      }
    },
    scales: {
      x: {
        ticks: {
          color: textColorSecondary
        },
        grid: {
          color: surfaceBorder
        }
      },
      y: {
        ticks: {
          color: textColorSecondary
        },
        grid: {
          color: surfaceBorder
        }
      }
    }
  }
}
</script>
