<template>
  <view class="navbar" :style="{ paddingTop: safeAreaInsets?.top + 'px' }">
    <!-- logo文字 -->
    <view class="logo">
      <image class="logo-image" src="@/static/images/logo.png" />
      <text class="logo-text"> · DoCheers · 去水印</text>
    </view>
    <!-- 搜索条 -->
    <view class="search"> </view>
  </view>
</template>
<script setup lang="ts">
//获取屏幕边界安全区域距离
const { safeAreaInsets } = uni.getSystemInfoSync()
</script>
<style lang="scss" scoped>
.navbar {
  background-image: url(@/static/images/navigator_bg.png);
  background-size: cover;
  position: relative;
  display: flex;
  flex-direction: column;
  padding: 40rpx;

  .logo {
    display: flex;
    align-items: center;
    height: 64rpx;
    padding-left: 64rpx;
    padding-top: 20rpx;

    .logo-image {
      width: 80rpx;
      height: 80rpx;
    }

    .logo-text {
      flex: 1;
      line-height: 28rpx;
      color: #fff;
      margin: 2rpx 0 0 20rpx;
      padding-left: 20rpx;
    }
  }
}
</style>
