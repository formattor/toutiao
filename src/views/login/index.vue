<template>
    <div class="login-container">
      <!-- 导航栏 -->
      <van-nav-bar class="page-nav-bar" title="登录">
        <van-icon slot="left" name="cross" @click="$router.back()"></van-icon>
      </van-nav-bar>
      <!-- 表单 -->
      <van-form @submit="onSubmit" ref="loginForm">
        <van-field
          name="mobile"
          placeholder="请输入手机号"
          v-model="user.mobile"
          :rules="userFormRules.mobile"
          type="number"
          maxlength="11"
        >
          <i slot="left-icon" class="toutiao toutiao-shouji"></i>
        </van-field>
        <van-field
          type="number"
          name="code"
          placeholder="请输入密码"
          v-model="user.code"
          :rules="userFormRules.code"
          maxlength="6"
        >
          <i slot="left-icon" class="toutiao toutiao-yanzhengma"></i>
          <template #button>
            <van-count-down v-if="isCountDownShow" :time="1000*10" format="ss s" @finish="isCountDownShow=false"/>
            <van-button v-else class="send-sms-btn" round size="small" type="default" @click="onSendSms" native-type="button">
              发送验证码
            </van-button>
          </template>
        </van-field>
        <div class="login-btn-wrap">
          <van-button class="login-btn" block type="info" native-type="submit">登录</van-button>
        </div>
      </van-form>
    </div>
</template>

<script type="text/ecmascript-6">
import { login, sendSms } from '@/api/user'
export default {
  name: 'LoginIndex',
  data () {
    return {
      user: {
        mobile: '13911111111',
        code: '246810'
      },
      userFormRules: {
        mobile: [{ required: true, message: '请填写手机号' }, {
          pattern: /^1[3|5|7|8]\d{9}$/,
          message: '手机号格式错误'
        }],
        code: [{ required: true, message: '请填写验证码' }, {
          // 臣妾做不到
          pattern: /^\d{6}$/,
          message: '验证码格式错误'
        }]
      },
      isCountDownShow: false
    }
  },
  created () {},
  components: {},
  methods: {
    async onSubmit () {
      // 获取表单数据
      const user = this.user
      // 表单验证
      this.$toast.loading({
        message: '登录中...',
        forbidClick: true,
        duration: 0
      })
      // 提交请求
      try {
        const { data: res } = await login(user)
        this.$toast.success('登录成功...')
        // console.log(res.data, 'vuex传进去没')
        this.$store.commit('setUser', res.data)
        // 不严谨
        this.$router.back()
      } catch (err) {
        if (err.response.status === 400) {
          this.$toast.fail('手机号或者验证码错误')
          console.log('手机号或者验证码错误', '')
        }
        console.log('登录失败', err)
      }
      // 响应结果处理后续操作
    },
    async onSendSms () {
      // 1.校验手机号码
      try {
        await this.$refs.loginForm.validate('mobile')
        console.log('验证通过', '')
      } catch (err) {
        return console.log('验证失败', 'err')
      }
      // 2.验证通过，显示倒计时
      this.isCountDownShow = true
      // 3.请求发生验证码
      try {
        await sendSms(this.user.mobile)
        this.$toast('成功')
      } catch (err) {
        this.isCountDownShow = false
        console.log('获取验证码失败', 'err')
        if (err.response.status === 429) {
          this.$toast('发送太频繁，请稍后重试')
        } else {
          this.$toast('发送失败')
        }
      }
    }
  }
}
</script>

<style lang="less" scoped>
.login-container{
  .toutiao{
    font-size: 37px;
  }
  .send-sms-btn {
    background-color: #ededed ;
    width: 152px;
    height: 46px;
    line-height: 46px;
    font-size: 22px;
    color: #666;
  }
  .login-btn-wrap{
    padding: 53px 33px;
    .login-btn{
      color: #6db4fb;
      border: none;
    }
  }
}
</style>
