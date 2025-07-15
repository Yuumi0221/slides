<script setup lang="ts">
defineProps<{
  title: string
  choices: {
    label: string
    do: () => void
  }[]
}>()
</script>

<template>
  <div class="text-4xl text-$ost-c-brand font-900 leading-normal">
    {{ title }}
  </div>

  <AdvChoices
    class="absolute bottom-0 left-0 right-0 top-10"
    :choices="choices"
  />
</template>
