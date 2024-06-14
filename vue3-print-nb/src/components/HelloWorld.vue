<script setup>
import { ref } from 'vue'

defineProps({
  msg: String,
})

const count = ref(0)

const tableData = [
  {
    date: '2016-05-03',
    name: 'Tom',
    address: 'No. 189, Grove St, Los Angeles',
  },
  {
    date: '2016-05-02',
    name: 'Tom',
    address: 'No. 189, Grove St, Los Angeles',
  },
  {
    date: '2016-05-04',
    name: 'Tom',
    address: 'No. 189, Grove St, Los Angeles',
  },
  {
    date: '2016-05-01',
    name: 'Tom',
    address: 'No. 189, Grove St, Los Angeles',
  },
]

const printObj = {
  id: 'printTable',
  // url: "http://localhost:5173/",
  preview:true,
  previewTitle: '打印预览',
  popTitle: 'good print',
  extraCss: "https://cdn.bootcdn.net/ajax/libs/animate.css/4.1.1/animate.compat.css, https://cdn.bootcdn.net/ajax/libs/hover.css/2.3.1/css/hover-min.css",
  extraHead: '<meta http-equiv="Content-Language"content="zh-cn"/>',
  beforeOpenCallback (vue) {
    console.log('打开之前')
  },
  openCallback (vue) {
    console.log('执行了打印')
  },
  closeCallback (vue) {
    console.log('关闭了打印工具')
  }
}
</script>

<template>
  <h1>{{ msg }}</h1>
  <div class="btn">
    <el-button type="primary" v-print="printObj">打印</el-button>
  </div>
  <el-table id="printTable" :data="tableData" border style="width: 100%">
    <el-table-column prop="date" label="Date" width="180" />
    <el-table-column prop="name" label="Name" width="180" />
    <el-table-column prop="address" label="Address" />
  </el-table>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
.btn {
  display: flex;
  justify-content: end;
  margin-bottom: 30px;
}
</style>
