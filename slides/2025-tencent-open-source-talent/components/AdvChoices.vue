<script setup lang="ts">
import { useSlideContext } from '@slidev/client'

defineProps<{
  choices: {
    label: string
    do: () => void
  }[]
}>()
</script>

<template>
  <div class="flex flex-col items-center justify-center h-full gap-8">
    <button
      v-for="choice in choices"
      :key="choice.label"
      class="rounded-none min-w-100 border-solid border-2px border-color-$ost-c-brand text-$ost-c-brand px-4 py-2 rounded hover:(bg-$ost-c-brand text-white) transition-colors"
      @click="choice.do"
    >
      {{ choice.label }}
    </button>
  </div>
</template>
