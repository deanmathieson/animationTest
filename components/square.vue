<template>
  <div ref="box" class="square" @click="changeColour"></div>
</template>

<script>
import gsap from "gsap";
export default {
  props: {
    count: {
      type: Number,
      default: 0,
    },
    delay: {
      type: Number,
      default: 0,
    },
  },
  mounted() {
    this.runAnimation();
  },
  methods: {
    getRandomInt(min, max) {
      min = Math.ceil(min);
      max = Math.floor(max);
      let rand = null;

      // while (rand === null || rand >= max / 2 || rand <= min / 2) {
      rand = Math.floor(Math.random() * (max - min) + min);
      // }

      return rand; //The maximum is exclusive and the minimum is inclusive
    },
    runAnimation() {
      console.log(this.delay * this.count);
      const { box } = this.$refs;
      gsap.to(box, {
        duration: 1,
        x: this.randomX,
        y: this.randomY,
        yoyo: true,
        repeat: -1,
        delay: this.delay * this.count,
        backgroundColor: this.colourGenerator(),
      });
    },
    colourGenerator() {
      return "#" + ((Math.random() * 0xffffff) << 0).toString(16);
    },
    changeColour() {
      const { box } = this.$refs;
      console.log(this);
      box.style.backgroundColor = this.colourGenerator();
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
  // watch: {
  //   duration(newValue, oldValue) {
  //     this.runAnimation();
  //   },
  // },
};
</script>

<style scoped>
.square {
  height: 40px;
  width: 40px;
  position: absolute;
  top: 50%;
  left: 50%;
  border-radius: 50%;
}
</style>