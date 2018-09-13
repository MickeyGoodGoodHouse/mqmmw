<template>
  <span class="tableComponents" >
    <table class="normalTable" :style="iStyle" >
      <tr>
        <th v-for="item in columns" :key="item.key" >{{item.title}}</th>
      </tr>
      <tr v-for="dataItem in Data" :key="dataItem.key" >
        <td v-for="columnsItem in dataItem" :key="columnsItem" >{{columnsItem}}</td>
      </tr>
    </table>
  </span>
</template>

<script>
import _ from "lodash";
export default {
  name: 'Table',
  props:{
    bordered:false,
    columns:Array,
    dataSource:Array,
    loading:false,
    iStyle:Object,
  },
  created: function () {
      let keys = _.keys(this.dataSource[0]);
      let Data = [];
      this.dataSource.map(ii=>{ 
          let dataItem = [];
        this.columns.map(gg=>{
          keys.map(vv=>{
            if(vv===gg.dataIndex){
              dataItem.push(ii[vv]);
            }
          });
        });
          Data.push(dataItem);
      });
      this.Data = Data;
  },
  data () {
    return {
      Data:[],
    }
  },
  directives: {
  },
  methods: {
  }
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
        border-bottom: 1px solid $colorGary;
    }
    th {
        background-color: $ThColor;
    }
}
</style>
