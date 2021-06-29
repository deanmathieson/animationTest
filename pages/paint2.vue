<template>
  <div ref="cont" class="cont" :style="{ backgroundColor: bgColor }">
    <div
      class="layer"
      @mouseup="mUp"
      @mousedown="mDown"
      @mousemove="triggerPaint"
      @click="triggerDraw"
    />
    <div class="options">
      <div>
        <input type="color" v-model="borderColor" />
        <label for="borderColor">border colour: {{ borderColor }}</label>
      </div>
      <div>
        <input type="color" v-model="color" />
        <label for="color">box colour: {{ color }}</label>
      </div>
      <div>
        <input type="color" v-model="bgColor" />
        <label for="bgColor">bg colour: {{ bgColor }}</label>
      </div>
      <div>
        <label for="size">Size!</label>
        <input type="number" v-model="size" min="1" max="300" step="10" />
      </div>
      <div>
        <label for="borderWidth">Border Width!</label>
        <input type="number" v-model="borderWidth" min="1" max="100" step="1" />
      </div>
      <div>
        <label for="radius">radius:</label>
        <input type="number" min="1" max="100" v-model="radius" step="10" />
      </div>
      <div>
        <label for="duration">duration:</label>
        <input type="number" min="1" max="100" v-model="duration" step="1" />
      </div>
      <div>
        <label for="x">x:</label>
        <input type="number" min="-1000" max="1000" v-model="x" step="100" />
      </div>
      <div>
        <label for="y">y:</label>
        <input type="number" min="-1000" max="1000" v-model="y" step="100" />
      </div>
      <div>
        <label for="easing">Easing: </label>
        <select v-model="easing">
          <option disabled value="">Please select one</option>
          <option v-for="ease in eases" :key="ease">{{ ease }}</option>
        </select>
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
      color: "#000000",
      mousedown: false,
      size: 20,
      radius: 50,
      counter: 0,
      duration: 5,
      bgColor: "#ffffff",
      borderWidth: 1,
      borderColor: "#e66465",
      x: 100,
      y: 100,
      timeStamp: 0,
      dotDelay: 20,
      easing: "elastic.out(1, .3)",
      eases: [
        "none",
        "power1.out",
        "power2.out",
        "power3.out",
        "power4.out",
        "back.out(1.7)",
        "elastic.out(1, .3)",
        "bounce.out",
        "slow(.7, .7, false)",
        "steps(10)",
        "circ.out",
        "expo.out",
        "sine.out",
      ],
    };
  },
  methods: {
    triggerPaint(e) {
      if (e.timeStamp >= this.timeStamp + this.dotDelay) {
        this.timeStamp = e.timeStamp;
        this.mouseX = e.pageX;
        this.mouseY = e.pageY;
      }
    },
    mDown() {
      this.mousedown = true;
    },
    mUp() {
      this.mousedown = false;
    },
    triggerDraw() {
      // if (this.mousedown) {
      let div = document.createElement("div");
      let className = ".item" + this.counter;
      div.classList.add("square");
      div.classList.add("item" + this.counter);
      div.style.left = this.mouseX - this.size / 2 + "px";
      div.style.top = this.mouseY - this.size / 2 + "px";
      div.style.width = this.size + "px";
      div.style.height = this.size + "px";
      div.style.borderRadius = this.radius + "px";
      div.style.border = this.borderWidth + "px solid " + this.borderColor;
      div.style.backgroundColor = this.color;
      document.body.appendChild(div);
      gsap.to(className, {
        x: this.x,
        y: this.y,
        opacity: 0,
        duration: this.duration,
        ease: this.easing,
        borderColor: this.colourGenerator(),
      });
      setTimeout(() => {
        document
          .querySelectorAll(className)[0]
          .parentNode.removeChild(document.querySelectorAll(className)[0]);
      }, this.duration * 1000);
      this.counter++;
      // }
    },
    colourGenerator() {
      return "#" + ((Math.random() * 0xffffff) << 0).toString(16);
    },
  },
  watch: {
    mouseX(newValue, oldValue) {
      this.triggerDraw();
    },
    bgColor(newValue, oldValue) {
      gsap.to(".cont", { backgroundColor: this.bgColor });
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
.square {
  position: absolute;
}
.options {
  z-index: 100;
  left: 0;
  top: 0;
  position: absolute;
  background-color: #ddd;
}
html {
  overflow: hidden;
}
</style>