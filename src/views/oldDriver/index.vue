<template>
  <div>
    <div class="searchBar" >
      <Input buttonText="嘀嘀嘀，开车啦" :iStyle="inputStyle" placeholder="震惊！小叉居然是变态" type="searchInput" />
    </div>
    <Table :columns="columns" :iStyle="tableStyle" :dataSource = "dataSource" />
  </div>
</template>

<script>
import Input from "@/components/global/input";
import Table from "@/components/global/table";
export default {
    name: "Header",
    components: {
        Input: Input,
        Table:Table,
    },
    data() {
        return {
          inputStyle:{
            marginBottom:"50px",
          },
          tableStyle:{
            width:"1000px",
            marginLeft: "calc(50% - 500px)",
          },
          columns:[{
            title: 'Name',
            dataIndex: 'name',
            key: 'name',
          }, {
            title: 'Age',
            dataIndex: 'age',
            key: 'age',
          }, {
            title: 'Address',
            dataIndex: 'address',
            key: 'address',
          }],
          dataSource:[{
            key: '1',
            name: 'John Brown',
            age: 32,
            address: 'New York No. 1 Lake Park',
            tags: ['nice', 'developer'],
          }, {
            key: '2',
            name: 'Jim Green',
            age: 42,
            address: 'London No. 1 Lake Park',
            tags: ['loser'],
          }, {
            key: '3',
            name: 'Joe Black',
            age: 32,
            address: 'Sidney No. 1 Lake Park',
            tags: ['cool', 'teacher'],
          }],
        };
    }
};
</script>

<style lang="scss">
.searchBar {
    width: 500px;
    display: inline-block;
}
</style>