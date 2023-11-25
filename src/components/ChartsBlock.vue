<template>
  <LineChart :data="data" :options="options" />
</template>

<script lang="ts">
import {
  Chart as ChartJS,
  CategoryScale,
  LinearScale,
  PointElement,
  LineElement,
  Title,
  Tooltip,
  Legend
} from 'chart.js'
import { Line as LineChart } from 'vue-chartjs'

ChartJS.register(
  CategoryScale,
  LinearScale,
  PointElement,
  LineElement,
  Title,
  Tooltip,
  Legend
)

export default {
props:{
  prefData:[],
  prefLabel:[]
},

  name: 'ChartsBlock',
  components: {
    LineChart
  },
  data() {
    return {
      data: {
  labels: this.preflabel,
  datasets: [
    this.prefData
  ]
},

 options: {
  responsive: true
}

    }
    
  }
}
</script>
