<template>
  <div>
    <div class="SubTitleArea">
      <h2>都道府県</h2>
    </div>
    <div id="CheckboxArea">
      <div id="CheckBoxAndLabelArea" v-for="(item, key) in prefectures" :key="key">
        <label for="checkbox">{{item.prefName}}</label>
        <input :value="item.prefCode" type="checkbox" class="Checkbox" v-model="checkedList" @change="onCheck($event,item.prefName,)">
      </div>
    </div>
  </div>
    
    
</template>

<script>


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
    onCheck(event,name){
      const data = {
        code:event.target.value,
        checked:event.target.checked,
        name:name
      }
      this.$emit("checkBoxChenged", data)
    }

  }

};

</script>

<style>

/* SubTitleAreaに当てるCSS */
.SubTitleArea h2{
  padding: 0.5rem 1rem;
  background: #f4f4f4;
  border-left: 4px dashed #27374D;
  margin: 0;
  color: #27374D;
}

.SubTitleArea{
  text-align: left;
  padding: 0px 40px;
  margin: 0;
}


/* CheckBoxAreaに当てるCSS */
  #CheckboxArea{
    background-color: #f4f4f4;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-wrap: wrap;
    border-radius: 20px;
    margin: 10px 36px 30px 36px;
    padding: 20px 0;
    height: 200px;
    overflow: scroll;
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

  #CheckBoxAndLabelArea label{
    font-size: 1.2rem;
    font-weight: bold;
    color: #27374D;
    width:fit-content;
  }

  #CheckBoxAndLabelArea input{
    transform:scale(1.2);
    width: fit-content;
  }

  .Checkbox{
    accent-color: #526D82;
  }


 /* スマホ用CSS */
  @media screen and (max-width: 414px){

    #CheckBoxAndLabelArea{
      display: flex;
      justify-content: center;
      align-items: center;
      width: calc(100% / 4);
      padding: 10px;
      text-align: left;
    }

    .SubTitleArea{
      text-align: left;
      padding: 0 22px;
      margin: 0;
    }

    .SubTitleArea h2{
      font-size: 1.2rem;
      padding: 0.2rem 1rem;
    }

    #CheckboxArea{
      height: 136px;
      overflow: scroll;
      margin: 10px 20px 24px 20px;
    }

    #CheckboxArea:after{
    width: calc(100% / 4);
    height: 0;
    padding: 10px;
}

    #CheckBoxAndLabelArea label{
      font-size: 1rem;
    }

    #CheckBoxAndLabelArea{
      width: calc(100% / 4);
    }

    /* #CheckboxArea:after{
    content: "";
    display: block;
    width: calc(100% / 4);
    height: 0;
    padding: 10px; */
}

</style>