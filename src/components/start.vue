<template>
    <div>
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
</template>

<script>
export default {

}
</script>

<style lang="less">
   #range {
       font-size: 14px;
       color: #ccc;
       margin-top: 10rpx;
       img {
           width: 20rpx;
           height: 20rpx;
       }
   }
</style>
