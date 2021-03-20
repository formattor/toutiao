<template>
    <div class="home-container">
      <!-- 头部标签 -->
      <van-nav-bar class="page-nav-bar">
        <van-button class="search-btn" icon="search" slot="title" type="info" size="small" round>搜索</van-button>
      </van-nav-bar>
      <!-- tab切换 -->
      <van-tabs class="channel-tabs" v-model="active" animated swipeable>
        <van-tab v-for="channel in channels" :key="channel.id" :title="channel.name">
          <ArticleList :channel="channel"></ArticleList>
        </van-tab>
        <div slot="nav-right" class="placeholder"></div>
        <div slot="nav-right" class="hamburger-btn">
          <i class="toutiao toutiao-gengduo"></i>
        </div>
      </van-tabs>
    </div>
</template>

<script type="text/ecmascript-6">
import { getuserChannels } from '@/api/user'
import ArticleList from './components/article-list'
export default {
  data () {
    return {
      active: 0,
      channels: []
    }
  },
  created () {
    this.loadChannels()
  },
  components: {
    ArticleList
  },
  methods: {
    async loadChannels () {
      try {
        const { data } = await getuserChannels()
        this.channels = data.data.channels
        console.log(this.channels, '获取成功')
      } catch (error) {
        this.$toast('获取频道数据失败')
      }
    }
  }
}
</script>

<style lang="less" scoped>
.home-container{
  padding-bottom: 100px;
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
