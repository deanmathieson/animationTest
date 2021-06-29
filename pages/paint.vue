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
        <label for="size">Size!</label>
        <input type="number" v-model="size" min="1" max="100" />
      </div>
      <div>
        <label for="radius">radius:</label>
        <input type="number" min="1" max="100" v-model="radius" />
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
      size: 20,
      radius: 50,
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
        div.style.width = this.size + "px";
        div.style.height = this.size + "px";
        div.style.borderRadius = this.radius + "px";
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
  left: 0;
  top: 0;
  position: absolute;
}
html {
  overflow: hidden;
}
</style>