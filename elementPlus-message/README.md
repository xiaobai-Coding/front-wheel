在实际的应用开发中，涉及用户登录验证、密码重置等场景时，通常需要前端实现发送短信验证码的功能，以提升用户体验和安全性。这个过程涉及与后端的协同配合，通过调用短信网关或短信服务接口，将验证码发送至用户手机。以下是一个简单的前端实现，演示了如何在用户点击发送验证码按钮时触发短信验证码的发送，并开始一个倒计时。
功能分析
遇事先认真分析是我今年在工作上的要求之一
将目标分解为小模块后再逐步完成。首先，我们需要一个手机号码输入框，并对输入的手机号码进行合法性校验。其次，需要一个验证码输入框，以及一个获取短信验证码的按钮。点击该按钮将向服务端发送获取请求，参数为输入的手机号码，并开始显示倒计时，倒计时结束后重新显示获取验证码按钮。服务端收到请求后会给该手机号码发送短信验证码，然后我们输入收到的验证码即可进行下一步操作。
项目使用vue3+vite+ElementPlus，这里假设你已经搭建好项目了！
页面实现
<el-form :model="form" label-width="120px">
  <el-form-item label="手机号码：">
    <el-input v-model="form.name" />
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

实现倒计时
点击获取验证码按钮将触发 sendCode 函数，开始倒计时，并隐藏获取按钮，显示倒计时的秒数，倒计时结束后会重新显示获取按钮。你可以通过修改 countdown 变量的值来指定倒计时的总秒数。 startCountdown 函数是整个功能的核心是直接可以拿来用的。最后在点击发送按钮的时候对手机号码输入框中的号码做一个校验。
const sendCode = () =>{
  const reg = /^1[3456789]\d{9}$/;
  if (!reg.test(form.value.phone)) return
  if(!form.value.phone) return ElMessage.error('请输入手机号码')
  countdown.value = 60
  messageCodeVis.value = true
  startCountdown()
}
/* 倒计时函数 */
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
全部代码
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
  countdown.value = 60
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
即使代码逻辑很简单，也值得记录下来。我的编程目标是避免重复造轮子！😊
祝小伙伴们新年快乐!🐉龙年大吉！
推荐一个AI生成红包封面的工具：https://github.com/all-in-aigc/aicover 
在线demo: https://aicover.design

有需要的小伙伴自己上手体验一下吧!
如果觉得有用，就给我点个赞吧😁
探索更多有趣知识，欢迎关注我的微信公众号！每天分享精彩内容，与你一同探寻知识的边界。扫码即可订阅，一起开启知识新旅程！🚀📚

关注我的技术博客，探索前沿科技与实用开发技巧。一起携手走向代码的精彩世界！🚀💻 不错过每一篇精彩！
https://www.xiaobaicoding.com
