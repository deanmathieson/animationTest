<template>
  <div class="cont bg-red-900">
    <div class="slider">
      <legend>count</legend>
      <input type="range" v-model="count" />
      <label for="count" min="1" max="1000" value="50">{{ count }}</label>
      <legend>duration</legend>
      <input type="range" v-model="duration" />
      <label for="duration">{{ duration }}</label>
    </div>
    <div v-for="square in parseInt(count)" :key="square">
      <square :duration="parseInt(duration)" />
    </div>
  </div>
</template>

<script>
import square from "@/components/square.vue";

export default {
  components: {
    square,
  },
  data() {
    return {
      count: 50,
      duration: 1,
    };
  },
};
</script>

<style>
.cont {
  width: 100vw;
  min-height: 100vh;
  display: flex;
}
.slider {
  position: absolute;
  z-index: 999;
}
</style>
