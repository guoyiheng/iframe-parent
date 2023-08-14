<script setup lang="ts" generic="T extends any, O extends any">
import { WindowChannel } from '@haiyaotec/window-channel'

defineOptions({
  name: 'IndexPage',
})

const originUrl = import.meta.env.DEV ? 'http://127.0.0.1:3334/' : 'https://iframe-child-gyh.vercel.app/'
const childUrl = ref(originUrl)
function refreshPage() {
  window.location.reload()
  refreshChildPage()
}
function refreshChildPage() {
  childUrl.value = localStorage.getItem('childUrl') || originUrl
}
onMounted(() => {
  refreshChildPage()
})
/**
 * serve
 */
const messageArr = ref<string[]>([])
const service = WindowChannel.newChannelService(window)
service.listen('/hello', (value: string) => {
  messageArr.value.push(value)
  const routerPath = value.split(': ')[1]
  localStorage.setItem('childUrl', routerPath)
  return `来自服务端消息${new Date().toLocaleTimeString()}: 接收成功`
})
</script>

<template>
  <div class="border-4px border-blue-300" p-10>
    <iframe class="h-300px w-full" :src="childUrl" frameborder="0" />

    <div m-3 c-blue-300>
      Parent Iframe
    </div>
    <button mb-20px btn @click="refreshPage">
      Refresh page
    </button>

    <ol w-full flex flex-col items-center justify-center gap-10px>
      <li v-for="item in messageArr" :key="item" class="w-400px border-1px p-4px">
        {{ item }}
      </li>
    </ol>
  </div>
</template>
