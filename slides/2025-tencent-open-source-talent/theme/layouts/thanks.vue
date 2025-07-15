<template>
  <div class="slidev-layout thanks">
    <img
      class="w-52 absolute top-10 left-12"
      src="/images/logo.webp"
      alt="犀牛鸟 Logo"
    >
    <div class="my-auto">
      <slot />
    </div>
  </div>
</template>

<style lang="scss">
.slidev-layout.thanks {
  background-color: #ebf6ff;

  background-image: url('/images/transparent-bg.webp');
  background-size: 765px 593px;
  background-position: right bottom;
  background-repeat: no-repeat;
  background-attachment: fixed;

  h1 {
    color: var(--ost-c-brand);
    font-weight: 900;
    font-family: 'TencentSans W7', 'TencentSans', sans-serif;
    font-size: 2.5rem;
  }
}
</style>
