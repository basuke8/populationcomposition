<template>
  <div class="SubTitleArea">
      <h2>総人口数</h2>
  </div>
  <div id="wrap-chart">
    <div id="ChartsContainer">
      <LineChart :data="data" :options="options"  :key="prefData.datasets.length"/>
    </div>  
  </div>
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
      responsive: true,
      maintainAspectRatio: false,
    }

  }
    
},

mounted() {

}

}
</script>

<style>
  #ChartsContainer{
      position: relative;
      width: calc(100vw - 60px);
      height: 650px;
      /* padding: 30px; */
      display: flex;
      justify-content: center;
      align-items: center;
    }

  #wrap-chart{
      width: 100%;
      height: 90vh;
      display: flex;
      justify-content: center;
      margin: 10px;
    }

/* スマホ用CSS */
  @media screen and (max-width: 414px){
    #ChartsContainer{
      position: relative;
      width: calc(100vw - 40px);
      height: 450px;
      display: flex;
      justify-content: center;
      align-items: center;
    }

    #wrap-chart{
      width: calc(100vw - 20px);
      height: 600px;
    }

    #ChartsContainer{

    }
    
  }  
</style>