<script setup lang="ts">
const childUrI = 'https://iframe-child-1.vercel.app/test'
</script>

<template>
  <div>
    <iframe :src="childUrI" frameborder="0"></iframe>
  </div>
</template>
