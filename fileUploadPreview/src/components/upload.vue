<template>
  <div class="upload-container">
    <!-- 图片上传 -->
    <div v-if="type === 'img'">
        <el-upload
          v-model:file-list="fileList"
          action=""
          :auto-upload="false"
          list-type="picture-card"
          :on-preview="handlePictureCardPreview"
          :on-remove="handleRemove"
          :on-change="onSuccess"
          :before-upload="beforeUpload"
          :limit="3"
        >
          <el-icon><Plus /></el-icon>
        </el-upload>
      <!-- 图片预览 -->
      <el-dialog v-model="dialogVisible">
        <img w-full :src="dialogImageUrl" alt="Preview Image" />
      </el-dialog>
    </div>
    <!-- 普通文件上传 -->
    <div v-else>
      <el-upload
        v-model:file-list="fileList"
        class="upload-demo"
        action=""
        multiple
        :on-preview="handlePreview"
        :on-remove="handleRemove"
        :before-remove="beforeRemove"
        :limit="3"
        :on-exceed="handleExceed"
      >
        <el-button type="primary">Click to upload</el-button>
        <template #tip>
          <div class="el-upload__tip">
            jpg/png files with a size less than 500KB.
          </div>
        </template>
      </el-upload>
    </div>
  </div>
</template>

<script setup>
import { ref, toRefs } from 'vue'
import { Plus } from '@element-plus/icons-vue'

const props = defineProps({
  type: {
    type: String,
    default: 'img'
  }
})
const { type } = toRefs(props)

const emit = defineEmits(['onChange'])
const fileList = ref([])

const dialogImageUrl = ref('')
const dialogVisible = ref(false)

const handleRemove = (uploadFile, uploadFiles) => {
  console.log(uploadFile, uploadFiles)
}

const handlePictureCardPreview = (uploadFile) => {
  dialogImageUrl.value = uploadFile.url
  dialogVisible.value = true
}

// 上传成功
const onSuccess = (file)=>{
  fileList.value.push(file.url)
  emit('onChange', fileList)
}
const beforeUpload = (file) =>{
  fileList.value.push(file)
  return false
}
</script>

<style lang="scss" scoped>

</style>