<script setup>
import { ref } from 'vue'
import { ElMessage } from 'element-plus';
const form = ref({
  phone: '',
  code: ''
})
const messageCodeVis = ref(false)
let countdown = ref(0)
const sendCode = () =>{
  const reg = /^1[3456789]\d{9}$/;
  if(!form.value.phone) return ElMessage.error('请输入手机号码')
  if (!reg.test(form.value.phone)) return
  countdown.value = 10
  messageCodeVis.value = true
  startCountdown()
}
/* 倒计时 */
const startCountdown = () => {
    const intervalId = setInterval(() => {
        if (countdown.value > 0) {
            countdown.value--;
        } else {
            clearInterval(intervalId)
            messageCodeVis.value = false
        }
    }, 1000)
}
const rulesForm = {
  phone: [
  { required: true, message: '请输入手机号码', trigger: 'blur' },
  { pattern: /^1[3456789]\d{9}$/, message: '请输入有效的手机号码', trigger: 'blur' }
  ]
}
</script>

<template>
    <el-form :model="form" :rules="rulesForm" label-width="120px">
      <el-form-item label="手机号码：" prop="phone">
        <el-input v-model="form.phone" />
      </el-form-item>
      <el-form-item label="验证码：">
        <el-input v-model="form.code" >
          <template #suffix>
            <div v-if="messageCodeVis" class="second-text">{{countdown}}秒后重新获取</div>
            <el-button v-else type="primary" link @click="sendCode">获取验证码</el-button>
          </template>
        </el-input>
      </el-form-item>
    </el-form>  
  <el-button type="primary">确定</el-button>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
.second-text {
  color: #e60707;
}
</style>
