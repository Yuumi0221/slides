<script setup lang="ts">
defineProps<{
  title: string
  author: string
  label?: string
  date?: string
}>()
</script>

<template>
  <div class="noto-serif-tc text-left text-$ost-c-brand font-900 leading-none absolute left-0 top-0 right-0 bottom-0 flex flex-col justify-center items-center">
    <div class="absolute left-20 bottom-15 text-8xl">
      {{ label }}
    </div>

    <div class="text-200px absolute top-15">
      {{ title }}
    </div>

    <div class="absolute text-xl right-20 bottom-15">
      {{ date }}
    </div>
  </div>
</template>
