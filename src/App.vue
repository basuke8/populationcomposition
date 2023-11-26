<script>
import CheckBoxBlock from "./components/CheckBoxBlock.vue";
import ChartsBlock from "./components/ChartsBlock.vue";
import axios from "axios";

export default {
  name: "App",
  components: {
    CheckBoxBlock,
    ChartsBlock
  },

  data(){
    return{
      graphData:{
        labels:["label1","label2"],
        datasets:[]
      },
      prefecturesData:[],
    }
  },
  mounted() {
    //都道府県一覧取得
    var prefectures_url =
      "https://opendata.resas-portal.go.jp/api/v1/prefectures";

    axios
      .get(prefectures_url, {
        headers: {
          "X-API-KEY": "eskC9CtGUPebeKah2vqeJszrylQrgjRUwua80bLN",
          "Content-Type": "application/json;charset=UTF-8",
        },
      })
      .then((response) => {
        this.prefecturesData = response.data.result;
        // console.log(response.data.result);
      });
  },

  methods: {
    getPopration(prefCode,prefname) {
      // 人口構成取得メソッド
      var population_url =
        "https://opendata.resas-portal.go.jp/api/v1/population/composition/perYear";

      axios
        .get(population_url, {
          params: { prefCode: prefCode, cityCode: "-" },
          headers: {
            "X-API-KEY": "eskC9CtGUPebeKah2vqeJszrylQrgjRUwua80bLN",
            "Content-Type": "application/json;charset=UTF-8",
          },
        })
        .then((response) => {
　　　　　　
          const randumDigit =　'#' + Math.floor(Math.random() * 1000)

          const prefData = {
            label: prefname,
            backgroundColor: randumDigit,
            data:response.data.result.data[0].data.map(v => v.value)
          }

          this.graphData.labels = response.data.result.data[0].data.map(v => v.year),
          this.graphData.datasets.push(prefData)
        });
    },

      //チェックボックがチェックされた時に走る処理
        checkBoxChenged(checkdata){
          if(checkdata.checked){
            this.getPopration(checkdata.code,checkdata.name)
          }else{
            this.graphData.datasets = this.graphData.datasets.filter((item) => item.label !== checkdata.name)
          } 
        }

  }

};
</script>

<template>
  <div id="TitleArea">
    <h1 id="Title">都道府県別人口推移</h1>
    <CheckBoxBlock  @checkBoxChenged = "checkBoxChenged"  :prefectures="prefecturesData"/>
    <!-- <ChartsBlock :prefData="populationTransfer" :prefLabel="prefLabel"/> -->
    <ChartsBlock :prefData="graphData"/>
  </div>
</template>

<style>
#TitleArea{
  text-align: center;
}

#Title{
  color: white;
  background-color: #27374D;
  padding: 20px;
  margin: 0 0 30px 0;
}
</style>
