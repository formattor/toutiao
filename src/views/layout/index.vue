<template>
    <div class="layout-container">
      <!-- 组件布局 -->
      <!-- 子路由出口 -->
      <router-view></router-view>
      <!-- 底部导航栏 -->
      <van-tabbar class="layout-tabbar" route>
        <van-tabbar-item to="/">
          <i slot="icon" class="toutiao toutiao-shouye"></i>
          <span>首页</span>
        </van-tabbar-item>
        <van-tabbar-item to="/qa">
          <i slot="icon" class="toutiao toutiao-wenda"></i>
          <span>问答</span>
        </van-tabbar-item>
        <van-tabbar-item to="/video">
          <i slot="icon" class="toutiao toutiao-shipin"></i>
          <span>视频</span>
        </van-tabbar-item>
        <van-tabbar-item to="/my">
          <i slot="icon" class="toutiao toutiao-wode"></i>
          <span>{{user?'我的':'未登录'}}</span>
        </van-tabbar-item>
      </van-tabbar>
    </div>
</template>

<script type="text/ecmascript-6">
import { mapState } from 'vuex'
export default {
  data () {
    return {
    }
  },
  created () {},
  components: {},
  methods: {},
  computed: {
    ...mapState(['user'])
  }
}
</script>

<style lang="less" scoped>
.layout-container{
  .layout-tabbar{
    i.toutiao{
      font-size: 40px;
    }
    span{
      font-size: 20px;
    }
  }
}
</style>
