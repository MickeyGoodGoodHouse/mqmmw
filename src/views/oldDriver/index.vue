<template>
  <div>
    <div class="searchBar" >
      <Input buttonText="嘀嘀嘀，开车啦" :iStyle="inputStyle" placeholder="震惊！小叉居然是变态" type="searchInput" :onClick="searchData" />
    </div>
    <Table :columns="columns" :iStyle="tableStyle" :dataSource = "dataSource" >
      <Input slot-scope="copy" buttonText="复制" type="searchInput" :defaultValue="copy.data" :onClick="copyUrl" />
    </Table>
  </div>
</template>

<script>
import Input from "@/components/global/input";
import Table from "@/components/global/table";
import axios from "axios";
export default {
    name: "Header",
    components: {
        Input: Input,
        Table:Table,
    },
    data() {
        return {
          defaultValue:"",
          inputStyle:{
            marginBottom:"50px",
          },
          tableStyle:{
            width:"80%",
            marginLeft: "10%",
          },
          columns:[{
            title: '种子名称',
            dataIndex: 'name',
            key: 'name',
          }, {
            title: '上架日期',
            dataIndex: 'date',
            key: 'date',
          }, {
            title: '链接地址',
            dataIndex: 'magnet',
            key: 'magnet',
            name:"one",
          }],
          dataSource:[],
        };
    },
    methods:{
      copyUrl(that){
        that.$refs.input.select();
        document.execCommand("Copy");;
      },
      searchData(that){
        let these = this;
        axios.post(`/olddriver/torrent_list`, {
            keyword: that.value,
        })
        .then(function (response) {
          let value = response.data;
          value.map(ii=>{
            ii.key = ii.id;
          });
          these.dataSource=value;
        })
        .catch(function (error) {
          console.log(error);
        });
      },
    }
};
</script>

<style lang="scss">
.searchBar {
    width: 500px;
    display: inline-block;
}
</style>