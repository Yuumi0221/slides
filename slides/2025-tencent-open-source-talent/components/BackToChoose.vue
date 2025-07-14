<script setup lang="ts">
function goBack() {
  window.history.back()
}
</script>

<template>
  <button
    text-2xl absolute bottom-15 font-bold text-center left-0 right-0
    class="rounded-none w-50 border-solid border-2px border-color-$ost-c-brand text-$ost-c-brand px-4 py-2 rounded hover:(bg-$ost-c-brand text-white) transition-colors m-auto"
    @click="goBack"
  >
    载入存档
  </button>
</template>
