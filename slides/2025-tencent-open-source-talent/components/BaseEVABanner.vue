<script setup lang="ts">
defineProps<{
  title: string
  author: string
  label?: string
  date?: string
}>()
</script>

<template>
  <div class="noto-serif-tc px-8 text-left text-$ost-c-brand font-900 leading-none mt-8">
    <div class="absolute right-4 top-4 m-2 text-xl">
      {{ label }}
    </div>

    <div class="m-2 text-72px">
      {{ author }}
    </div>

    <div class="text-144px">
      {{ title[0] }}
    </div>

    <div class="text-144px">
      {{ title.slice(1) }}
    </div>

    <div class="absolute m-2 text-xl">
      {{ date }}
    </div>
  </div>
</template>
