<template>
  <div class="cont">
    <div class="slider">
      <legend>count</legend>
      <input type="range" v-model="count" min="1" max="500" />
      <label for="count">{{ count }}</label>
      <!-- <legend>duration</legend>
      <input type="range" v-model="duration" min=".1" max="5" step=".1" />
      <label for="duration">{{ duration }}</label> -->
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
  top: 0;
  left: 0;
}
</style>
