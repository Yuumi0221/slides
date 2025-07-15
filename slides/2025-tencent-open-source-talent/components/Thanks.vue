<script setup lang="ts">
import { nextTick, onMounted, ref } from 'vue'

const couplets = ref(
  [
    [
      '万物有趣',
      '开源大吉',
    ],
    // [
    //   '数据源幻境',
    //   '自动化真章',
    // ],
  ],
)

let i = 0
const curCouplet = ref(couplets.value[i])

const show = ref(false)

// const interval = 5000
onMounted(() => {
  show.value = true
  // setInterval(async () => {
  //   i++
  //   const index = i % couplets.value.length
  //   curCouplet.value = couplets.value[index]

  //   show.value = false
  //   await nextTick()
  //   show.value = true
  // }, interval)
})
</script>

<template>
  <div class="text-6xl font-bold top-0 bottom-0 left-12 right-12 flex flex-col  items-center justify-center absolute text-$ost-c-brand">
    THANKS

    <div class="w-120 mt-8" flex="~ col gap-2 items-center justify-center">
      <img class="shadow size-40 rounded" src="/images/2025_02_05_19_59_二维码（多人领取）.png" alt="小云红包封面">
      <div text-xs class="text-#ed6c51 font-black">
        扫码领取小云红包封面
      </div>
    </div>
  </div>

  <div
    v-motion
    class="absolute bottom-0 left-0"
    :initial="{ x: -50, y: '100%' }"
    :enter="{ x: 0, y: '0%', transition: { duration: 500 } }"
  >
    <img class="w-50" src="/images/小云广告位招租.webp" alt="小云广告位招租">
    <Transition name="fade">
      <div
        v-if="show"
        class="absolute right-36px top-152px z-1 rotate-18 text-md text-yellow font-bold tracking-widest write-vertical-left"
      >
        {{ curCouplet[0] }}
      </div>
    </Transition>
  </div>

  <div
    v-motion
    class="absolute bottom-0 right-0"
    :initial="{ x: 50, y: '100%' }"
    :enter="{ x: 0, y: '0%', transition: { duration: 500 } }"
  >
    <img class="w-50 -scale-x-100" src="/images/小云广告位招租.webp" alt="小云广告位招租">
    <Transition name="fade">
      <div
        v-if="show"
        class="absolute left-35px top-152px z-1 text-lg text-yellow font-bold tracking-widest write-vertical-left -rotate-18"
      >
        {{ curCouplet[1] }}
      </div>
    </Transition>
  </div>
</template>
