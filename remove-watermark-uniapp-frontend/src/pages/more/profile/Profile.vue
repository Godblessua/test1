<template>
  <view class="viewport">
    <!-- 导航栏 -->
    <view class="navbar" :style="{ paddingTop: safeAreaInsets?.top + 'px' }"> </view>
    <view class="avatar">
      <view class="avatar-content">
        <text v-if="!isLogin" class="image" @tap="login"> 登 录 </text>
        <image v-if="isLogin" :src="iconUrl" mode="aspectFit" />
      </view>
    </view>
    <!-- 列表1 -->
    <view class="list">
      <button hover-class="none" class="item arrow" open-type="openSetting">授权管理</button>
      <button hover-class="none" class="item arrow" open-type="feedback">问题反馈</button>
      <button hover-class="none" class="item arrow" open-type="contact">联系我们</button>
    </view>
    <!-- 列表2 -->
    <view class="list">
      <navigator hover-class="none" class="item arrow" url=" ">关于XXX</navigator>
    </view>
    <!-- 操作按钮 -->
    <view class="action">
      <view class="button" @tap="logout">退出登录</view>
    </view>
  </view>
</template>
<script setup lang="ts">
import { ref } from 'vue'

// 获取屏幕边界到安全区域距离
const { safeAreaInsets } = uni.getSystemInfoSync()

const iconUrl = ref('/static/images/logo.png')
//制作一个假登录
const isLogin = ref(false)
const login = () => {
  isLogin.value = true
  setTimeout(() => {
    uni.showToast({ icon: 'success', title: '登录成功' })
  })
}

//退出登录
const logout = () => {
  isLogin.value = false
  setTimeout(() => {
    uni.showToast({ icon: 'success', title: '退出登录' })
  })
}
</script>

<style lang="scss">
page {
  background-color: #f4f4f4;
}

.viewport {
  display: flex;
  flex-direction: column;
  height: 100%;
  background-image: url(@/static/images/profile_bg.png);
  background-size: auto 420rpx;
  background-repeat: no-repeat;
}

// 导航栏
.navbar {
  position: relative;

  .title {
    height: 40px;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 16px;
    font-weight: 500;
    color: #fff;
  }

  .back {
    position: absolute;
    height: 40px;
    width: 40px;
    left: 0;
    font-size: 20px;
    color: #fff;
    display: flex;
    justify-content: center;
    align-items: center;
  }
}

.avatar {
  text-align: center;
  width: 100%;
  height: 260rpx;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  .avatar-content {
    cursor: point;
    width: 150rpx;
    height: 150rpx;
    background-color: #fff;
    box-shadow: 0rpx 0rpx 6rpx 6rpx #2a54a7;
    border-radius: 50%;
    .image {
      font-size: 36rpx;
      font-weight: bold;
      color: #1e8ea1;
      line-height: 150rpx;
    }
  }
}

/* 列表 */
.list {
  padding: 0 20rpx;
  background-color: #fff;
  margin-bottom: 20rpx;
  border-radius: 10rpx;
  .item {
    line-height: 90rpx;
    padding-left: 10rpx;
    font-size: 30rpx;
    color: #333;
    border-top: 1rpx solid #ddd;
    position: relative;
    text-align: left;
    border-radius: 0;
    background-color: #fff;
    &::after {
      width: auto;
      height: auto;
      left: auto;
      border: none;
    }
    &:first-child {
      border: none;
    }
    &::after {
      right: 5rpx;
    }
  }
  .arrow::after {
    content: '\e6c2';
    position: absolute;
    top: 50%;
    color: #ccc;
    font-family: 'erabbit' !important;
    font-size: 32rpx;
    transform: translateY(-50%);
  }
}

/* 操作按钮 */
.action {
  text-align: center;
  line-height: 90rpx;
  margin-top: 40rpx;
  font-size: 32rpx;
  color: #333;
  .button {
    background-color: #fff;
    margin-bottom: 20rpx;
    border-radius: 10rpx;
  }
}
</style>
