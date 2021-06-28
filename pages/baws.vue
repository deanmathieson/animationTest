<template>
  <div ref="cont" class="cont">
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
import gsap from "gsap";
export default {
  components: {
    square,
  },
  data() {
    return {
      count: 50,
      delay: 0.2,
      rand: this.colourGenerator(),
      rand2: this.colourGenerator(),
    };
  },
  computed: {
    gradient() {
      return "linear-gradient(" + this.rand + ", " + this.rand2 + ")";
    },
  },
  methods: {
    colourGenerator() {
      return "#" + ((Math.random() * 0xffffff) << 0).toString(16);
    },
  },
  mounted() {
    const { cont } = this.$refs;

    gsap.to(cont, {
      yoyo: true,
      repeat: -1,
      duration: 10,
      backgroundColor: this.colourGenerator(),
      backgroundImage: this.gradient,
    });
  },
};
</script>

<style>
.slider {
  position: absolute;
  z-index: 999;
  top: 0;
  left: 0;
}
</style>
