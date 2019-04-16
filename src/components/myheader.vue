<template>
    <div class="headTop">
        <div class="le">
            <a hover-class="none" class="title" href="#">豆瓣</a>
            <a hover-class="none" class="title" href="#">
                <icon type="search" size="20" color="#42bd56" />
            </a>
        </div>
        <div class="right">
            <button>打开豆瓣App</button>
        </div>
    </div>
</template>

<script>
export default {

}
</script>

<style lang="less">
@color:#42bd56;
.headTop {
    height: 94rpx;
    padding: 0 35rpx;
    display: flex;
    line-height: 94rpx;
    justify-content: space-between;
    border-bottom: 1px solid #ccc;
    .left {
        display: flex;
        .title {
            color: @color;
            font-size: 30px;
            font-weight: 700;
            margin-right: 35rpx;
        }
        .search {
            margin-top: 10rpx;
        }
    }
    .right {
        button {
            background-color: @color;
            color: #fff;
            font-size: 16px;
            padding: 0rpx 20rpx;
            margin-top: 10rpx;
        }
    }
}

</style>
