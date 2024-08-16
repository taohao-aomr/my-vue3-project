<template>
  <view class="content">
    <image class="logo" src="/static/logo.png"></image>
    <view class="text-area b-1px b-solid b-color-red">
      <text class="title mt-4">{{ title }}</text>
      <text class="title mt-4">{{ title }}</text>
      <button type="primary" @click="useCountStore.count++">点击 {{ count }}</button>
    </view>

    <view class="content">
    <view><button type="primary" @click="getList">点击请求数据</button></view>
  </view>
  <view class="p-2">
    <view
      class="my-15rpx b-b-solid b-b-1rpx b-b-color-[#cccccc]"
      v-for="item in list"
      :key="item.id"
    >
      <text class="text-18rpx font-bold">{{ item.title }}</text>
      <view class="mt-4 text-12rpx color-[#9999]">{{ item.body }}</view>
    </view>
  </view>
  </view>
</template>

<script setup>
import { useOutsideCountStore } from '@/store/count'
const useCountStore = useOutsideCountStore()
const count = computed(() => useCountStore.count)

const title = ref('Hello World!')

const { API_DEMO_GET } = useRequest()
  const list = ref([])

  const getList = () => {
    uni.showLoading({
      title: '加载中...'
    })
    API_DEMO_GET()
      .then((res) => {
        console.log(res)
        list.value = res
        uni.hideLoading()
      })
      .catch(() => {
        uni.hideLoading()
      })
  }
</script>


<style>
.content {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.logo {
  height: 200rpx;
  width: 200rpx;
  margin-top: 200rpx;
  margin-left: auto;
  margin-right: auto;
  margin-bottom: 50rpx;
}

.text-area {
  display: flex;
  justify-content: center;
}

.title {
  font-size: 36rpx;
  color: #8f8f94;
}
</style>
