<template>
<div>
  <!-- 头部部分 -->
  <myheader></myheader>
  <!-- 电影部分 -->
   <div class="moveList">
     <div class="title">{{title}}</div>
     <div class="list">
       <div class="item" v-for="(item,index) in dataList" :key="index">
         <img :src="item.images.small" alt="">
         <div class="name">{{item.title}}</div>
         <start :startnum ="item.rating.average"></start>       
         </div>
     </div>
   </div>
    <div class="foot" v-if="isEnd == true">
        我是有底线的
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
  data(){
    return{
      data:{
        start:0,
        count:9,
        city:"深圳"
      },
      dataList:[],
      title:'',
      query:{},
      isEnd:false
    }
  },
  methods: {
    async getDataList(){
      //在导航中添加加载动画
      wx.showNavigationBarLoading()
      if(this.isEnd){
        wx.showToast({
          title: '数据已经加载完毕',
          icon: 'none',
          duration: 2000
        })
        return
      }
      //打开加载动画
      wx.showLoading({
        title:'加载中'
      })
      //得到请求的列表数据
      this.query = this.$root.$mp.query;
      switch(this.query.type){
        case 'in-theaters':
        this.title = '热映电影'
        break;
        case 'top250':
        this.title = '经典电影'
        break;
      }
      var res = await myrequest({
        url:'https://douban.uieee.com/v2/movie/'+this.query.type,
        data:this.data,
        header:{
          'content-type':'json'
        }
      })
      if(res.data.subjects.length == 0){
        //提示用户已经加载完了
         wx.showToast({
          title: '数据已经加载完毕',
          icon: 'none',
          duration: 2000
        })
        this.isEnd = true;
        return;
      }
      if(this.dataList.length==0){
        this.dataList = res.data.subjects;
      }else{
        //将之前赋值的存在的数组在拼接到新的数组中
        this.dataList = this.dataList.concat(res.data.subjects);
      }
      //关闭加载框
      wx.hideLoading()
      //关闭下拉框
       wx.stopPullDownRefresh();
       //关闭导航加载
       wx.hideNavigationBarLoading();
    }
  },
  //接收参数
  mounted() {
    this.getDataList()
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
