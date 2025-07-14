<script setup lang="ts">
defineProps<{
  title: string
}>()
</script>

<template>
  <div class="text-left absolute top-36 left-12">
    <h1 class="relative">
      {{ title || '从犀牛鸟开「园」到三顾鹅厂' }}
      <div class="absolute left-63 text-base -top-7">
        源
      </div>
    </h1>
    <h2 class="text-$ost-c-brand">
      2025 腾讯犀牛鸟开源分享
    </h2>
  </div>

  <div class="speaker-info absolute bottom-12 left-12 text-$ost-c-brand">
    <div class="text-left font-bold">
      杨睿（云游君）
      <br>
      腾讯微信前端工程师
      <br>
      2025年6月26日
    </div>
  </div>
</template>
