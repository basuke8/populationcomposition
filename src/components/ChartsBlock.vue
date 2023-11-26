<template>
  <LineChart :data="data" :options="options"  :key="prefData.datasets.length"/>
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
  prefData:[]
},

  name: 'ChartsBlock',
  components: {
    LineChart
  },
data() {
  return {
    data:
      this.prefData
    ,
    options: {
      responsive: true
    }

  }
    
},

mounted() {

}

}
</script>
