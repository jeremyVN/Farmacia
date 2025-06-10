<template>
  <Bar :data="chartData" :options="chartOptions" />
</template>

<script setup>
import { Bar } from 'vue-chartjs'
import { Chart, BarElement, CategoryScale, LinearScale, Tooltip, Legend } from 'chart.js'
import { computed } from 'vue'

Chart.register(BarElement, CategoryScale, LinearScale, Tooltip, Legend)

const props = defineProps({
  labels: Array,
  values: Array,
  label: String
})

// Computamos los datos reactivos
const chartData = computed(() => ({
  labels: props.labels,
  datasets: [
    {
      label: props.label,
      backgroundColor: '#3b82f6',
      data: props.values,
    }
  ]
}))

const chartOptions = computed(() => ({
  responsive: true,
  plugins: {
    legend: { display: false }
  }
}))
</script>
