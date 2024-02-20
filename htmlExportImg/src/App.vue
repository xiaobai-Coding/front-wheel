<script setup>
import html2canvas from 'html2canvas';
import HelloWorld from './components/HelloWorld.vue'
const exportImg = () =>{
  const dom = document.getElementById('exportContainer')
  exportToImage(dom, 'vue3+vite')
}
/**
 * @description 将dom对象导出为图片
 * @param {Object} exportContent 要导出的内容
 * @param {String} title 导出的图片名称
 */
 const exportToImage = (exportContent, title)=> {
  html2canvas(exportContent).then((canvas) => {
    const imageDataUrl = canvas.toDataURL('image/png');
    const downloadLink = document.createElement('a');
    downloadLink.href = imageDataUrl;
    downloadLink.download = `${title}.png`;
    downloadLink.click();
  });
}
</script>

<template>
  <div style="padding: 20px" id="exportContainer">
    <div>
    <a href="https://vitejs.dev" target="_blank">
      <img src="/vite.svg" class="logo" alt="Vite logo" />
    </a>
    <a href="https://vuejs.org/" target="_blank">
      <img src="./assets/vue.svg" class="logo vue" alt="Vue logo" />
    </a>
  </div>
  <HelloWorld msg="将html导出为图片" />
  </div>
  <div class="card">
    <button type="button" class="btn" @click="exportImg">导出为图片</button>
  </div>
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
.card .btn {
  background-color: #409eff;
  border-color: #409eff;
  color: #fff;
}
</style>
