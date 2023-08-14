<script setup lang="ts">
const childUrI = 'https://iframe-child-1.vercel.app'
function refreshPage() {
  window.location.reload()
}
</script>

<template>
  <div border-1px p-10>
    <iframe :src="childUrI" frameborder="0" />
    <div>Parent Iframe</div>
    <button
    btn
      @click="refreshPage"
    >
      Refresh page
    </button>
  </div>
</template>
