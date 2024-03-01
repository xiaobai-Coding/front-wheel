<script setup>
import QrcodeVue from 'qrcode.vue'
const level = ref('M')
const renderAs = ref('svg')
import { ref } from 'vue'
const link = ref('https://www.mi.com/')
// 下载二维码
const downloadQrCode = () =>{
   const node = document.getElementById('svgRef')
   covertSVG2Image(node, '扫描二维码，分享此链接', 120, 120)
}
/**
 * 将svg导出成图片
 * @param node svg节点 => document.querySelector('svg')
 * @param name 生成的图片名称
 * @param width 生成的图片宽度
 * @param height 生成的图片高度
 * @param type 生成的图片类型
 */
 const covertSVG2Image = (node, name, width, height, type = 'png') => {
  let serializer = new XMLSerializer()
  let source = '<?xml version="1.0" standalone="no"?>\r\n' + serializer.serializeToString(node)
  let image = new Image()
  image.src = 'data:image/svg+xml;charset=utf-8,' + encodeURIComponent(source)
  let canvas = document.createElement('canvas')
  canvas.width = width
  canvas.height = height
  let context = canvas.getContext('2d')
  context.fillStyle = '#fff'
  context.fillRect(0, 0, 10000, 10000)
  image.onload = function () {
    context.drawImage(image, 0, 0)
    let a = document.createElement('a')
    a.download = `${name}.${type}`
    a.href = canvas.toDataURL(`image/${type}`)
    a.click()
  }
}
</script>

<template>
  <h1>前端实现链接生成二维码</h1>
  <el-input v-model="link" placeholder="Please input" style="width: 400px;">
      <template #append>
        <el-popover
        placement="bottom"
        :width="160"
        trigger="click"
      >
        <template #reference>
          <div class="qrcode">二维码</div>
        </template>
        <template #default>
          <div class="code-container">
            <div class="title">扫描二维码，分享此链接</div>
            <qrcode-vue id="svgRef" :value="link" :size="120" :level="level" :render-as="renderAs" />
            <el-button style="width: 120px;margin-top: 10px;" class="m-t10" size="small" @click="downloadQrCode">下载</el-button>
          </div>
        </template>
      </el-popover>
      </template>
  </el-input>
</template>

<style scoped>
.code-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.qrcode {
  cursor: pointer;
}
.title {
  font-size: 12px;
  color: #8e939c;
  margin-bottom: 5px;
}
</style>
