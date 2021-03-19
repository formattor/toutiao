<template>
    <div class="home-container">
      <!-- 头部标签 -->
      <van-nav-bar class="page-nav-bar">
        <van-button class="search-btn" icon="search" slot="title" type="info" size="small" round>搜索</van-button>
      </van-nav-bar>
      <!-- tab切换 -->
      <van-tabs class="channel-tabs" v-model="active" animated swipeable>
        <van-tab title="标签 1">内容 1</van-tab>
        <van-tab title="标签 2">内容 2</van-tab>
        <van-tab title="标签 3">内容 3</van-tab>
        <van-tab title="标签 4">内容 4</van-tab>
        <van-tab title="标签 4">内容 4</van-tab>
        <van-tab title="标签 4">内容 4</van-tab>
        <div slot="nav-right" class="placeholder"></div>
        <div slot="nav-right" class="hamburger-btn">
          <i class="toutiao toutiao-gengduo"></i>
        </div>
      </van-tabs>
    </div>
</template>

<script type="text/ecmascript-6">
export default {
  data () {
    return {
      active: 0
    }
  },
  created () {},
  components: {},
  methods: {}
}
</script>

<style lang="less" scoped>
.home-container{
  /deep/.van-nav-bar__title{
    max-width: unset;
  }
  .search-btn{
    width: 555px;
    height: 64px;
    background-color: #5babfb;
    border: none;
    font-size: 28px;
    /deep/.van-icon{
      font-style: 32px;
    }
  }
  /deep/ .channel-tabs{
    .van-tabs__wrap{
      height: 82px;
    }
    .van-tab{
      min-width: 200px;
      border-right: 1px solid #edeff3;
      font-style: 30px;
      color: #777;
    }
    .van-tab--active{
      color:#333
    }
    .van-tabs__nav{
      padding-bottom: 0;
    }
    .van-tabs__line{
      width: 31px;
      height: 6px;
      background-color: #3296fa;
      bottom: 8px;
    }
    .hamburger-btn{
      position: fixed;
      right: 0;
      width: 66px;
      height: 82px;
      display: flex;
      justify-items: center;
      align-items: center;
      background-color: #fff;
      opacity:0.902;
      i.toutiao{
        font-size: 33px;
      }
      &:before{
        content: "";
        width: 1px;
        height: 100%;
        background-image: url(~@/assets/gradient-gray-line.png);
        position: absolute;
        left: -40%;
        // left: 0;
        background-size: contain;
      }
    }
    .placeholder{
      width: 92px;
      height: 82px;
      flex-shrink: 0;
    }
  }
}
</style>
