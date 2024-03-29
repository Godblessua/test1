<template>
  <!-- 视频去水印卡片 -->
  <view class="card">
    <!-- 卡片标题头部 -->
    <view class="card-head">
      <view class="head-lf">
        <image class="img-icon" :src="imageUrl" mode="aspectFit" />
        <text class="title">{{ title }}</text>
      </view>
      <view class="head-rh">
        <image class="img-icon" src="../../static/images/logo.png" mode="aspectFit" />
      </view>
    </view>
    <!-- 卡片内容部分 -->
    <view class="card-content">
      <slot></slot>
    </view>
  </view>
</template>
<script setup lang="ts">
defineProps<{
  title: string
  imageUrl: string
}>()
</script>
<style lang="scss" scoped>
.card {
  background-color: #fff;
  border-radius: 16rpx;
  box-shadow: 0 4rpx 8rpx rgba(0, 0, 0, 0.1); /* 添加阴影效果 */
  // padding: 16rpx; /* 设置内边距 */
  margin: 16rpx; /* 设置外边距 */
  .card-head {
    display: flex;
    justify-content: space-between;
    padding: 24rpx 24rpx;
    border-bottom: 2rpx solid #cac9c9;
    .head-lf {
      display: flex;
      .title {
        font-size: 32rpx;
        margin-left: 30rpx;
        line-height: 90rpx;
      }
    }
    .img-icon {
      width: 90rpx;
      height: 90rpx;
    }
  }
  .card-content {
    padding: 32rpx;
  }
}
</style>
