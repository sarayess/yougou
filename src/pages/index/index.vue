<template>
<div>
  <!-- 头部部分 -->
  <myheader></myheader>
  <!-- 电影部分 -->
  <div class="box">
    <div class="title">
      <div class="work">影院热映</div>
      <div class="more">
        <a href="/pages/list/main?type=in_theaters">更多</a>
      </div>
    </div>
    <!-- 使用小程序中的滚动组件 -->
    <scroll-view scroll-x class="list">
       <div class="item">
         <img src="https://img1.doubanio.com/view/photo/m_ratio_poster/public/p2551352209.jpg" alt="">
         <div class="name">老师好</div>
          
       </div>
       <div class="item"  v-for="(item,index) in hotList" :key="index">
         <img :src="item.images.small" alt="">
         <div class="name">{{item.name}}</div>
          <start startnum = "item.rating.average"></start>
       </div>
   </scroll-view>
  </div>
  <div class="box">
    <div class="title">
      <div class="work">经典电影</div>
      <div class="more">
        <a href="/pages/list/main?type=top250">更多</a>
      </div>
    </div>
    <!-- 使用小程序中的滚动组件 -->
    <scroll-view scroll-x class="list">
       <div class="item">
         <img src="https://img1.doubanio.com/view/photo/m_ratio_poster/public/p2551352209.jpg" alt="">
         <div class="name">老师好</div>
          <div v-if="startnum != 0" id="range">
            <img v-if="startnum/2 > 0" src="../../static/images/a.png" alt="">
            <img v-else src="../../static/images/b.png" alt="">
             <img v-if="startnum/2 > 1" src="../../static/images/a.png" alt="">
             <img v-else src="../../static/images/b.png" alt="">
             <img v-if="startnum/2 > 2" src="../../static/images/a.png" alt="">
             <img v-else src="../../static/images/b.png" alt="">
             <img v-if="startnum/2 > 3" src="../../static/images/a.png" alt="">
             <img v-else src="../../static/images/b.png" alt="">
             <img v-if="startnum/2 > 4" src="../../static/images/a.png" alt="">
             <img v-else src="../../static/images/b.png" alt="">
        </div>
        <div v-else>暂无评分</div>
       </div>
       <div class="item"  v-for="(item,index) in hotList" :key="index">
         <img :src="item.images.small" alt="">
         <div class="name">{{item.title}}</div>
          <start :startnum ="item.rating.average"></start>
       </div>
   </scroll-view>
  </div>
  </div>
</template>

<script>
//引入头部组件
import myheader from '../../components/myheader'
//引入自定义组件
import myrequest from '../../utils/myrequest.js'
import start from '../../components/start'

export default {
  data:{
    hotList:[],
    oldList:[]
  },
  //请求热映数据
  methods: {
    async gethotList(){
      var res = await myquest({
        url:"http://douban.wangboqing.top/v2/movie/in_theaters",
        methods:'get',
        data:{
          start:0,
          count:6,
          city:'深圳'
        },
        header:{
          'content-type':'json'
        }
      })
      this.hotList = res.data.subjects
    },
    //请求经典数据
    async getoldList(){
      var res = await myrequest({
        url:'http://douban.wangboqing.top/v2/movie/top250',
        data:{
          start:0,
          count:6
        },
        methods:'get',
        header:{
          'content-type':'json'
        }
      })
      this.oldList = res.data.subjects;
    }
  },
  mounted() {
    //将异步代码改造为同步方式
    this.getoldList()
    this.gethotList()
  },
  //注册组件
  components:{
    myheader,
    start
  }
  }

  
</script>

<style lang="less">
  @color: #42bd56;
.box {
  .title {
    height: 98rpx;
    padding: 0 35rpx;
    display: flex;
    justify-content: space-between;
    font-size: 20px;
    line-height: 98rpx;
    .more {
      color: @color;
    }
  }
  .list {
    width: 100%;
    white-space: nowrap;
    .item {
      width: 200rpx;
      height: 400rpx;
      display: inline-block;
      margin-right: 16rpx;
      text-align: center;
      &:first-child {
        margin-left: 35rpx;
      }
      &:last-child {
        margin-right: 35rpx;
      }
      img {
        width: 200rpx;
        height: 286rpx;
      }
      .name {
        font-size: 16px;
        overflow: hidden;
        /*超出部分隐藏*/
        white-space: nowrap;
        /*不换行*/
        text-overflow: ellipsis;
        /*超出部分文字以...显示*/
      }
    }
  }
}
</style>
