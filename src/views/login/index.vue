<template>
    <div class="login-container">
      <!-- 导航栏 -->
      <van-nav-bar class="page-nav-bar" title="登录" />
      <!-- 表单 -->
      <van-form @submit="onSubmit">
        <van-field
          name="用户名"
          placeholder="请输入手机号"
        >
          <i slot="left-icon" class="toutiao toutiao-shouji"></i>
        </van-field>
        <van-field
          type="password"
          name="验证码"
          placeholder="请输入密码"
        >
          <i slot="left-icon" class="toutiao toutiao-yanzhengma"></i>
          <template #button>
            <van-button class="send-sms-btn" round size="small" type="default">发送验证码</van-button>
          </template>
        </van-field>
        <div class="login-btn-wrap">
          <van-button class="login-btn" block type="info" native-type="submit">登录</van-button>
        </div>
      </van-form>
    </div>
</template>

<script type="text/ecmascript-6">
export default {
  name: 'LoginIndex',
  data () {
    return {
      username: '',
      password: ''
    }
  },
  created () {},
  components: {},
  methods: {
    onSubmit (values) {
      console.log('submit', values)

      // 获取表单数据

      // 表单验证
      // 提交请求
      // 响应结果处理后续操作
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
