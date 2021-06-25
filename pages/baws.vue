<template>
  <div class="cont">
    <div class="slider">
      <legend>count</legend>
      <input type="range" v-model="count" min="1" max="500" />
      <label for="count">{{ count }}</label>
      <legend>delay</legend>
      <input type="range" v-model="delay" min=".1" max="1" step=".1" />
      <label for="delay">{{ delay }}</label>
    </div>
    <div v-for="square in parseInt(count)" :key="square">
      <square :delay="parseFloat(delay).toFixed(1)" :count="square" />
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
      delay: 0.2,
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
  top: 0;
  left: 0;
}
</style>
