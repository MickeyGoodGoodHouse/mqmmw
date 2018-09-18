<template>
  <div>
    <Banner :scrolled ="scrolled" />
    <div class="searchBar" >
      <Input buttonText="嘀嘀嘀，开车啦" buttonType="primary" :iStyle="inputStyle" :placeholder="placeholder" type="searchInput" :onClick="searchData" />
    </div>
    <Spin :spining="loading" >
      <Table :columns="columns" :iStyle="tableStyle" :dataSource = "dataSource" :noDataText="noDataText"  >
        <Input slot-scope="copy"  buttonText="复制" type="searchInput" :defaultValue="copy.data" :onClick="copyUrl" />
      </Table>
    </Spin>
  </div>
</template>

<script>
import Input from "@/components/global/input";
import Table from "@/components/global/table";
import Spin from "@/components/global/spin";
import Banner from "@/components/business/banner";
import axios from "axios";
export default {
    name: "Header",
    components: {
        Input: Input,
        Table:Table,
        Spin:Spin,
        Banner:Banner,
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
          loading:false,
          placeholder:"震惊！小叉居然是变态",
          noDataText:"",
          scrolled:false,
          scrollBefore:0,
        };
    },
    created:function(){
        const  these = this;
        const defaultArry = ["寻梦环游记","死侍2","蚁人2","我不是药神","你的名字","声之形"];
        let num = Math.round(Math.random()*(defaultArry.length-1));
        this.placeholder = defaultArry[num];
        this.loading = true;
        axios.post(`/olddriver/torrent_list`, {
                keyword: defaultArry[num],
            })
            .then(function (response) {
              let value = response.data?response.data:response.result;
              Array.isArray(value)?value.map(ii=>{
                ii.key = ii.id;
              }):these.noDataText=value.result;
              these.dataSource = [];
              if(Array.isArray(value)){
                these.dataSource=value;
                these.noDataText=null;
              }
              these.loading=false;
            })
            .catch(function (error) {
              console.log(error);
            });
            
      window.addEventListener('scroll', this.handleScroll);
    },
    methods:{
      handleScroll () {
        this.scrolled = (window.scrollY - this.scrollBefore) > 0;
        this.scrollBefore = window.scrollY;
      },
      copyUrl(that){
        that.$refs.input.select();
        document.execCommand("Copy");;
      },
      searchData(that){
        this.loading = true;
        let these = this;
        if(!that.value){
          this.placeholder = "你搜你🐎呢";
          this.loading=false;
        }else{
            axios.post(`/olddriver/torrent_list`, {
                keyword: that.value,
            })
            .then(function (response) {
              let value = response.data?response.data:response.result;
              Array.isArray(value)?value.map(ii=>{
                ii.key = ii.id;
              }):these.noDataText=value.result;
              these.dataSource = [];
              if(Array.isArray(value)){
                these.dataSource=value;
                these.noDataText=null;
              }
              // Array.isArray(value)?these.dataSource=value:null;
              these.loading=false;
            })
            .catch(function (error) {
              console.log(error);
            });
        }
      },
    }
};
</script>

<style lang="scss">
.searchBar {
    width: 80%;
    max-width: 500px;
    display: inline-block;
    margin-top: 120px;
}
</style>