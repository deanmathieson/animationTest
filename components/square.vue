<template>
  <div ref="box" class="square"></div>
</template>

<script>
import gsap from "gsap";
export default {
  props: {
    duration: {
      type: Number,
      default: 1,
    },
  },
  mounted() {
    this.runAnimation();
  },
  methods: {
    getRandomInt(min, max) {
      min = Math.ceil(min);
      max = Math.floor(max);
      return Math.floor(Math.random() * (max - min) + min); //The maximum is exclusive and the minimum is inclusive
    },
    runAnimation() {
      const { box } = this.$refs;
      gsap.to(box, {
        duration: this.duration,
        x: this.randomX,
        y: this.randomY,
        yoyo: true,
        repeat: -1,
        backgroundColor: this.generator(),
      });
    },
    generator() {
      return "#" + ((Math.random() * 0xffffff) << 0).toString(16);
    },
  },
  computed: {
    randomY() {
      let maxY = document.querySelectorAll(".cont")[0].scrollHeight / 2 - 40;
      return this.getRandomInt(-maxY, maxY);
    },
    randomX() {
      let maxX = document.querySelectorAll(".cont")[0].scrollWidth / 2 - 40;
      return this.getRandomInt(-maxX, maxX);
    },
  },
  watch: {
    duration(newValue, oldValue) {
      this.runAnimation();
    },
  },
};
</script>

<style scoped>
.square {
  height: 40px;
  width: 40px;
  background-color: purple;
  position: absolute;
  top: 50%;
  left: 50%;
}
</style>