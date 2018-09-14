<template>
  <span class="tableComponents" >
    <table class="normalTable" :style="iStyle" >
      <tr>
        <th v-for="item in columns" :key="item.key" >{{item.title}}</th>
      </tr>
      <tr v-for="dataItem in Data" :key="dataItem.key" >
        <td v-for="columnsItem in dataItem" :key="typeof(columnsItem)==='object'?columnsItem.value:columnsItem" >
          <slot v-if="typeof(columnsItem)==='object'" :data="columnsItem.value" ></slot> 
          {{typeof(columnsItem)!=='object'?columnsItem:null}}
        </td>
      </tr>
    </table>
  </span>
</template>

<script>
import _ from "lodash";
// import TableInput from "./tableInput.vue";
import Input from "../input";
export default {
  name: 'Table',
  components: {
        Input:Input,
        // TableInput:TableInput,
    },
  props:{
    bordered:false,
    columns:Array,
    dataSource:Array,
    loading:false,
    iStyle:Object,
  },
  watch:{
    dataSource:function(){
      let keys = _.keys(this.dataSource[0]);
      let Data = [];
      this.dataSource.map(ii=>{ 
        let dataItem = [];
        this.columns.map(gg=>{
          keys.map(vv=>{
            if(gg.name){
              if(vv===gg.dataIndex){
                let value = {};
                value.name = gg.name;
                value.value = ii[vv];
                dataItem.push(value);
              }
            }else{
              if(vv===gg.dataIndex){
                dataItem.push(ii[vv]);
              }
            }
          });
        });
          Data.push(dataItem);
      });
      this.Data = Data;
    },
  },
  data () {
    return {
      Data:[],
      dataSourceValue : this.dataSource,
    }
  },
}
</script>

<style lang="scss">
$colorGary: rgb(232, 232, 232);
$ThColor: rgb(250, 250, 250);
.normalTable {
    width: auto;
    text-align: center;
    border-collapse: collapse;
    tr,
    th,
    td {
        padding: 16px;
        max-width:300px;
        overflow: hidden;
        border-bottom: 1px solid $colorGary;
    }
    th {
        background-color: $ThColor;
    }
}
</style>
