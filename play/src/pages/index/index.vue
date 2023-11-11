<script setup lang="ts">
import { ref } from 'vue'
import TnButton from '@tuniao/tnui-vue3-uniapp/components/button/src/button.vue'
import TnUpdateUserInfoPopup from '../../packages/src/index.vue'

const showPopup = ref<boolean>(false)
const nickname = ref<string>('')
const avatar = ref<string>('')

// 头像选择事件
const avatarChooseHandle = (url: string) => {
  uni.uploadFile({
    url: 'https://vue3service.tuniaokj.com/upload/image',
    fileType: 'image',
    filePath: url,
    name: 'file',
    success: (res) => {
      const data = JSON.parse(res.data)
      avatar.value = data.data.url
    },
  })
}
</script>

<template>
  <view class="content">
    <TnButton @click="() => (showPopup = true)"> 修改用户信息 </TnButton>
  </view>

  <TnUpdateUserInfoPopup
    v-model:show="showPopup"
    v-model:nickname="nickname"
    v-model:avatar="avatar"
    @choose-avatar="avatarChooseHandle"
  />
</template>

<style lang="scss" scoped>
.content {
  position: relative;
  width: 100vw;
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;

  .message {
    font-size: 50rpx;
  }
}
</style>
