<script setup lang="ts" generic="T extends any, O extends any">
defineOptions({
  name: 'IndexPage',
})

const name = ref('')

const router = useRouter()
function go() {
  if (name.value)
    router.push(`/hi/${encodeURIComponent(name.value)}`)
}

const childUrI = 'https://iframe-child-1.vercel.app'
function refreshPage() {
  window.location.reload()
}
</script>

<template>
  <div class="border-1px" p-10>
    <iframe class="h-300px w-full" :src="childUrI" frameborder="0" />

    <div m-3>
      Parent Iframe
    </div>
    <button btn @click="refreshPage">
      Refresh page
    </button>
    <!-- <TheInput
      v-model="name"
      placeholder="What's your name?"
      autocomplete="false"
      @keydown.enter="go"
    />
    <div>
      <button class="m-3 text-sm btn" :disabled="!name" @click="go">
        Go
      </button>
    </div> -->
  </div>
</template>
