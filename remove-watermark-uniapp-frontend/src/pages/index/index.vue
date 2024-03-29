<template>
  <Navbar />
  <RwSwiper />
  <RwCard :title="title" :image-url="iconUrl">
    <view class="url-content">
      <!-- <input class="input" placeholder="请粘贴视频链接" /> -->
      <view class="input">
        <input
          class="uni-input"
          placeholder="请粘贴视频链接"
          :value="urlValue"
          @input="clearInput"
        />
        <uni-icons
          class="clear-icon"
          v-if="showClearIcon"
          @click="clearIcon"
          type="clear"
          size="30"
        ></uni-icons>
      </view>
      <!-- <text class="uni-icon" v-if="showClearIcon" @click="clearIcon">&#xe434;</text> -->
      <button class="button" type="primary" @tap="submitVideoUrl">提 交</button>
    </view>
    <view class="download-content">
      <view class="download">
        <view class="tips">{{ isGetVideo ? '处理完成✅，请下载!!!' : '暂无可下载视频' }}</view>
        <button class="button" type="primary" @tap="uploadVideo" :disabled="!isGetVideo">
          下 载
        </button>
      </view>
    </view>
  </RwCard>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import Navbar from './components/Navbar.vue'
import RwCard from './components/RwCard.vue'
import { getRwVideoAPI } from '@/api/RwVideo'

const title = ref('视频去水印')
const iconUrl = ref('/static/images/videoIcon.png')

//链接
const urlValue = ref<any>('')

//是否清除输入
const showClearIcon = ref(false)

//清除输入
const clearInput = (e: any) => {
  urlValue.value = e.detail.value
  if (e.detail.value.length > 0) {
    showClearIcon.value = true
  } else {
    showClearIcon.value = false
  }
}

//点击清除
const clearIcon = () => {
  urlValue.value = ''
  showClearIcon.value = false
}

//是否提取到原始视频
const isGetVideo = ref(false)

const RwVideoHD = ref()
//提交需要去水印视频链接
const submitVideoUrl = async () => {
  const res = await getRwVideoAPI(urlValue.value)
  //@ts-ignore
  if (res.message === 'success') {
    //@ts-ignore
    RwVideoHD.value = res.data.video_data.nwm_video_url
    isGetVideo.value = true
  } else {
    uni.showToast({ icon: 'fail', title: '视频提取失败!!!' })
  }
}

//下载视频
const uploadVideo = () => {
  // uni.showToast({ icon: 'loading', title: '下载中' })
  const downloadTask = uni.downloadFile({
    url: RwVideoHD.value, //文件下载路径
    success: (res) => {
      console.log('res-->>', res)
      if (res.statusCode === 200) {
        uni.saveVideoToPhotosAlbum({
          filePath: res.tempFilePath,
          success: function () {
            uni.showToast({
              title: '视频保存成功',
            })
          },
          fail: function (error) {
            uni.showToast({
              title: '取消视频保存',
              icon: 'none',
            })
          },
        })
      } else {
        uni.showToast({
          title: '下载视频失败',
          icon: 'none',
        })
      }
    },
    fail: function (error) {
      uni.showToast({
        title: '下载视频失败：' + error.errMsg,
        icon: 'none',
      })
    },
  })
  downloadTask.onProgressUpdate((res) => {
    const progress = Math.floor(res.progress) // 计算下载进度的百分比
    uni.showToast({
      title: '下载进度：' + progress + '%',
      icon: 'loading',
      duration: 2000,
    })

    // 满足测试条件，取消下载任务。
    // if (res.progress > 50) {
    // 	downloadTask.abort();
    // }
  })
}
</script>

<style lang="scss">
page {
  background-color: #f7f7f7;
  height: 100%;
  display: flex;
  flex-direction: column;
}
.url-content {
  display: flex;
  justify-content: space-between;
  .input {
    display: flex;
    align-items: center;
    padding: 16rpx;
    border-radius: 10rpx;
    border: 2rpx solid #cac9c9;
    height: 80rpx;
    line-height: 80rpx;
    width: 400rpx;
    .uni-input {
      font-size: 30rpx;
      height: 80rpx;
      line-height: 80rpx;
    }
    .clear-icon {
      margin-top: 12rpx;
      .uniui-clear {
        color: #cac9c9 !important;
        font-size: 45rpx !important;
      }
    }
  }
  .button {
    font-size: 32rpx;
    line-height: 80rpx;
    margin: 0rpx;
    min-width: 200rpx;
  }
}
.download-content {
  margin-top: 30rpx;
  .download {
    display: flex;
    justify-content: space-between;
    .tips {
      font-size: 30rpx;
      height: 80rpx;
      line-height: 80rpx;
      margin-left: 14rpx;
      color: #919191;
    }
    .button {
      font-size: 32rpx;
      line-height: 80rpx;
      min-width: 200rpx;
      margin: 0rpx;
    }
  }
}
</style>
