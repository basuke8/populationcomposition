<script>
import CheckBoxBlock from "./components/CheckBoxBlock.vue";
import ChartsBlock from "./components/ChartsBlock.vue";
import axios from "axios";
import { Colors } from 'chart.js';

export default {
  name: "App",
  components: {
    CheckBoxBlock,
    ChartsBlock
  },

  data(){
    return{
      prefecturesData:[],
      populationTransfer:[],
      prefLabel:[]
    }
  },
  mounted() {
    //都道府県一蘭取得
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
        console.log(response.data.result);
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
          this.prefLabel = response.data.result.data[0].data.map(v => v.year)

          const prefData = {
            label: prefname,
            backgroundColor: "#27374D",
            data:response.data.result.data[0].data.map(v => v.value)
          }
          this.populationTransfer.push(prefData)
          alert(this.populationTransfer.map((value) => value.label));

          // this.prefectures = response.data.result
        });
    },

      //チェックボックがチェックされた時に走る処理
        checkBoxChenged(checkdata){
            // alert(checkdata)
            //データがあるかどうか判定Todo
            this.populationTransfer.forEach((value) => {
              if(value.label == checkdata.name){
                  return
              }
            })
            
            this.getPopration(checkdata.code,checkdata.name)
        }

  }

};
</script>

<template>
  <div id="TitleArea">
    <h1 id="Title">都道府県別人口推移</h1>
    <CheckBoxBlock  @checkBoxChenged = "checkBoxChenged"  :prefectures="prefecturesData"/>
    <ChartsBlock :prefData="prefData" :preflabel="prefLabel"/>
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
