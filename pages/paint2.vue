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
        <label for="alpha">alpha</label>
        <input
          type="range"
          id="alpha"
          v-model="alpha"
          min="0"
          max="1"
          step="0.1"
          value="1"
        />
      </div>
      <div>
        <label for="size">Size!</label>
        <input type="number" v-model="size" min="1" max="300" step="10" />
      </div>
      <div>
        <label for="borderWidth">Border Width!</label>
        <input type="number" v-model="borderWidth" min="0" max="100" step="1" />
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
        <label for="rotation">Rotation:</label>
        <input
          type="number"
          min="-360"
          max="360"
          v-model="rotation"
          step="10"
        />
      </div>
      <div>
        <label for="easing">Easing: </label>
        <select v-model="easing">
          <option disabled value="">Please select one</option>
          <option v-for="ease in eases" :key="ease.name">
            {{ ease.name }}
          </option>
        </select>
      </div>
      <div>
        <label for="shape">Shapes: </label>
        <select v-model="selectedShape">
          <option disabled value="">Please select one</option>
          <option v-for="shape in shapes" :key="shape.name">
            {{ shape.name }}
          </option>
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
      size: 200,
      counter: 0,
      duration: 30,
      bgColor: "#000000",
      borderWidth: 1,
      borderColor: "#e66465",
      x: 100,
      y: 100,
      timeStamp: 0,
      dotDelay: 20,
      easing: "elastic in",
      eases: [
        {
          name: "Ease",
          value: "none",
        },
        {
          name: "power1",
          value: "power1.out",
        },
        {
          name: "power2",
          value: "power2.out",
        },
        {
          name: "power3",
          value: "power3.out",
        },
        {
          name: "power4",
          value: "power4.out",
        },
        {
          name: "back out",
          value: "back.out(1.7)",
        },
        {
          name: "elastic out",
          value: "elastic.out(1, .3)",
        },
        {
          name: "elastic in",
          value: "elastic.in(1, .3)",
        },
        {
          name: "elastic in out",
          value: "elastic.inout(1, .3)",
        },
        {
          name: "bounce out",
          value: "bounce.out",
        },
        {
          name: "slow",
          value: "slow(.7,}{ .7,}{ false)",
        },
        {
          name: "10steps",
          value: "steps(10)",
        },
        {
          name: "circle out",
          value: "circle.out",
        },
        {
          name: "expo",
          value: "expo.out",
        },
        {
          name: "sine",
          value: "sine.out",
        },
      ],
      shapes: [
        {
          name: "square",
          clip: "",
        },
        {
          name: "triangle",
          clip: "polygon(50% 0%, 0% 100%, 100% 100%)",
        },
        {
          name: "trapezoid",
          clip: "polygon(20% 0%, 80% 0%, 100% 100%, 0% 100%)",
        },
        {
          name: "pentagon",
          clip: "polygon(50% 0%, 100% 38%, 82% 100%, 18% 100%, 0% 38%)",
        },
        {
          name: "hexagon",
          clip: "polygon(25% 0%, 75% 0%, 100% 50%, 75% 100%, 25% 100%, 0% 50%)",
        },
        {
          name: "arrow",
          clip: "polygon(40% 0%, 40% 20%, 100% 20%, 100% 80%, 40% 80%, 40% 100%, 0% 50%)",
        },
        {
          name: "star",
          clip: "polygon(50% 0%, 61% 35%, 98% 35%, 68% 57%, 79% 91%, 50% 70%, 21% 91%, 32% 57%, 2% 35%, 39% 35%)",
        },
        {
          name: "X",
          clip: "polygon(20% 0%, 0% 20%, 30% 50%, 0% 80%, 20% 100%, 50% 70%, 80% 100%, 100% 80%, 70% 50%, 100% 20%, 80% 0%, 50% 30%)",
        },
        {
          name: "cross",
          clip: "polygon(10% 25%, 35% 25%, 35% 0%, 65% 0%, 65% 25%, 90% 25%, 90% 50%, 65% 50%, 65% 100%, 35% 100%, 35% 50%, 10% 50%)",
        },
        {
          name: "circle",
          clip: "circle(50% at 50% 50%)",
        },
      ],
      rotation: 360,
      alpha: 1,
      selectedShape: "hexagon",
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
      div.style.border = this.borderWidth + "px solid " + this.borderColor;
      div.style.backgroundColor = this.color;
      div.style.opacity = this.alpha;
      this.shapes.forEach((shape) => {
        if (shape.name === this.selectedShape) {
          div.style.clipPath = shape.clip;
        }
      });
      let easing = "";
      this.eases.forEach((ease) => {
        if (ease.name === this.easing) {
          easing = ease.value;
        }
      });
      document.body.appendChild(div);
      console.log(easing);
      gsap.to(className, {
        x: this.x,
        y: this.y,
        opacity: 0,
        duration: this.duration,
        ease: easing,
        borderColor: this.colourGenerator(),
        backgroundColor: this.colourGenerator(),
        rotation: this.rotation,
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