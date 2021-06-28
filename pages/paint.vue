<template>
  <div ref="cont" class="cont">
    <div
      class="layer"
      @mouseup="mUp"
      @mousedown="mDown"
      @mousemove="triggerPaint"
    />
    <div class="options">
      <div>
        <input type="color" v-model="color" />
        <label for="color">{{ color }}</label>
      </div>
      <div>
        <label for="height">Height!</label>
        <input type="number" v-model="height" min="1" max="100" />
        <label for="width">Width!</label>
        <input type="number" v-model="width" min="1" max="100" />
      </div>
    </div>
  </div>
</template>

<script>
import gsap from "gsap";
export default {
  data() {
    return {
      mouseX: "50vh",
      mouseY: "50vw",
      color: "#e66465",
      mousedown: false,
      width: 20,
      height: 20,
    };
  },
  methods: {
    triggerPaint(e) {
      this.mouseX = e.pageX;
      this.mouseY = e.pageY;
    },
    mDown() {
      console.log("mouse is down!");
      this.mousedown = true;
    },
    mUp() {
      console.log("mouse is up!");
      this.mousedown = false;
    },
  },
  watch: {
    mouseX(newValue, oldValue) {
      if (this.mousedown) {
        let div = document.createElement("div");
        div.classList.add("square");
        div.style.left = this.mouseX + "px";
        div.style.top = this.mouseY + "px";
        div.style.width = this.width + "px";
        div.style.height = this.height + "px";
        div.style.backgroundColor = this.color;
        document.body.appendChild(div);
      }
    },
  },
};
</script>

<style>
.layer {
  width: 100vw;
  height: 100vh;
  position: absolute;
  z-index: 99;
}
.cont {
  background-color: red;
}
.square {
  position: absolute;
}
.options {
  z-index: 100;
}
</style>