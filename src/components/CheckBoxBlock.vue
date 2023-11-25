<template>
  <div>
    <div id="SubTitleArea">
      <h2>都道府県</h2>
    </div>
    <div id="CheckboxArea">
      <div id="CheckBoxAndLabelArea" v-for="(item, key) in prefectures" :key="key">
        <label for="Checkbox">{{item.prefName}}</label>
        <input type="Checkbox" id="Checkbox" v-model="checkedList" @change="onCheck">
      </div>
    </div>
  </div>
    
    
</template>

<script>
import axios from "axios";
import { watch } from 'vue';

export default {
  //必要なデータを取得コンポーネント使用時引数として使用可
  props:{
    prefectures:[],
  },

  data() {
    return {
      checkedList:[]
    };
  },
  mounted() {
  },

  methods:{
    onCheck(){
      this.$emit("checkBoxChenged", this.checkedList)
    }

  }

};

</script>

<style>

/* SubTitleAreaに当てるCSS */
h2{
  padding: 0.5rem 1rem;
  background: #f4f4f4;
  border-left: 4px dashed #27374D;
  margin: 0;
  color: #27374D;
}

#SubTitleArea{
  text-align: left;
  padding: 10px 40px;
  margin: 0;
}


/* CheckBoxAreaに当てるCSS */
  #CheckboxArea{
    background-color: #f4f4f4;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-wrap: wrap;
    /* border: solid 3px #526D82; */
    border-radius: 20px;
    margin: 10px 36px;
    padding: 20px 0;
  }

  #CheckBoxAndLabelArea{
    display: flex;
    justify-content: center;
    align-items: center;
    width: calc(100% / 7);
    padding: 10px;
    text-align: left;
  }

  #CheckboxArea:after{
    content: "";
    display: block;
    width: calc(100% / 7);
    height: 0;
    padding: 10px;
}

  label{
    font-size: 1.2rem;
    font-weight: bold;
    color: #27374D;
    width:fit-content;
  }

  input{
    transform:scale(1.2);
    width: fit-content;
  }

  #Checkbox{
    accent-color: #526D82;
  }

</style>