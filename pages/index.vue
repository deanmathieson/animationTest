<template>
  <div class="cont" ref="cont">
    <p class="text-7xl pb-5">oh aye theres hings here</p>
    <nuxt-link to="baws">
      <button
        class="
          bg-blue-500
          hover:bg-blue-700
          text-white
          font-bold
          py-2
          px-4
          rounded
        "
      >
        Baws R Here
      </button></nuxt-link
    >
    <nuxt-link to="paint">
      <button
        class="
          bg-blue-500
          hover:bg-blue-700
          text-white
          font-bold
          py-2
          px-4
          rounded
        "
      >
        painty R Here
      </button></nuxt-link
    >
    <nuxt-link to="paint2">
      <button
        class="
          bg-blue-500
          hover:bg-blue-700
          text-white
          font-bold
          py-2
          px-4
          rounded
        "
      >
        painty2 R Here
      </button></nuxt-link
    >
  </div>
</template>

<script>
export default {
  data() {
    return {
      count: 50,
      duration: 1,
    };
  },
};
</script>

<style>
</style>
