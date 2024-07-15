<script setup>
import { ref } from 'vue'
import upload from "./components/upload.vue"
const activeName = ref('img')

const onChange = (e) =>{
  console.log(e)
}
</script>

<template>
  <div>
    <a href="https://vitejs.dev" target="_blank">
      <img src="/vite.svg" class="logo" alt="Vite logo" />
    </a>
    <a href="https://vuejs.org/" target="_blank">
      <img src="./assets/vue.svg" class="logo vue" alt="Vue logo" />
    </a>
  </div>
  <!-- 文件上传 -->
  <el-tabs v-model="activeName" class="demo-tabs" @tab-click="handleClick">
    <el-tab-pane label="图片上传" name="img">
      <upload :type="activeName" @onChange="onChange" />
    </el-tab-pane>
    <el-tab-pane label="文件上传" name="file">
      <upload :type="activeName" @onChange="onChange" />
    </el-tab-pane>
  </el-tabs>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
