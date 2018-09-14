<template>
  <Input defaultValue="666" />
</template>

<script>
import _ from "lodash";
import Input from "../input"
export default {
  name: 'Table',
  components: {
    Input: Input,
  },
  props:{
    defaultValue:"",
    type:"",
    buttonText:"",
    iStyle:Object,
    placeholder:"",
    search:Function,
    defaultValue:"",
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
  },
  directives: {
  },
  methods: {
  }
}
</script>

<style lang="scss">
</style>
