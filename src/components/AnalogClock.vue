<template>
  <div class="clock-frame">
    <div class="hour-hand" :style="hourHandStyle">
      <div class="hour-hand-tip" />
    </div>
    <div class="minute-hand" :style="minuteHandStyle">
      <div class="minute-hand-tip" />
    </div>
    <div class="second-hand" :style="secondHandStyle">
      <div class="second-hand-tip" />
    </div>
    <div class="center-circle" />
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  data() {
    return {
      hourHandStyle: {
        transform: "",
      },
      minuteHandStyle: {
        transform: "",
      },
      secondHandStyle: {
        transform: "",
      },
      nowHours: 0,
      nowMinutes: 0,
      nowSeconds: 0,
    };
  },
  async mounted() {
    const d = new Date();
    this.nowSeconds = d.getSeconds() * 1000;
    this.nowMinutes = d.getMinutes();
    this.nowHours = d.getHours();
    this.updateClock();
  },
  methods: {
    updateClock() {
      setInterval(() => {
        const d = new Date();
        const now = d.getSeconds() * 1000 + d.getMilliseconds();
        if (this.nowSeconds > 59000 && now < 1000) {
          this.nowSeconds = 0;
          this.nowMinutes = d.getMinutes();
          this.nowHours = d.getHours();
          this.secondHandStyle.transform = "rotate(0deg)";
          this.minuteHandStyle.transform = `rotate(${this.nowMinutes * 6}deg)`;
          this.hourHandStyle.transform = `rotate(${this.nowHours * 30 + this.nowMinutes / 2}deg)`;
        } else if (now > this.nowSeconds) {
          this.nowSeconds = now;
          this.secondHandStyle.transform = `rotate(${(now / 1000) * 6}deg)`;
          this.minuteHandStyle.transform = `rotate(${this.nowMinutes * 6 + this.nowSeconds / 10000}deg)`;
          this.hourHandStyle.transform = `rotate(${
            this.nowHours * 30 + (this.nowMinutes * 60000 + this.nowSeconds) / 120000
          }deg)`;
        }
      }, 1);
    },
  },
});
</script>

<style scoped>
.clock-frame {
  --clock-size: min(500px, calc(100vw - 30px), calc(100vh - 30px));
  width: var(--clock-size);
  height: var(--clock-size);
  border: 5px solid black;
  border-radius: 50%;
  position: relative;
  margin: 10px auto;
  background-image: url("/analog-clock.png");
  background-size: cover;
}
.hour-hand {
  position: absolute;
  width: 100%;
  height: 100%;
}
.hour-hand-tip {
  position: absolute;
  top: calc(50% - var(--clock-size) * 0.3);
  left: calc(50% - 5px);
  width: 10px;
  height: calc(var(--clock-size) * 0.3);
  background-color: black;
  transform-origin: bottom;
}
.minute-hand {
  position: absolute;
  width: 100%;
  height: 100%;
}
.minute-hand-tip {
  position: absolute;
  top: calc(50% - var(--clock-size) * 0.4);
  left: calc(50% - 3px);
  width: 6px;
  height: calc(var(--clock-size) * 0.4);
  background-color: black;
  transform-origin: bottom;
}
.second-hand {
  position: absolute;
  width: 100%;
  height: 100%;
}
.second-hand-tip {
  position: absolute;
  top: calc(50% - var(--clock-size) * 0.48);
  left: calc(50% - 1px);
  width: 2px;
  height: calc(var(--clock-size) * 0.48);
  background-color: black;
  transform-origin: bottom;
}
.center-circle {
  position: absolute;
  top: calc(50% - var(--clock-size) * 0.015);
  left: calc(50% - var(--clock-size) * 0.015);
  width: calc(var(--clock-size) * 0.03);
  height: calc(var(--clock-size) * 0.03);
  border-radius: 50%;
  background-color: black;
}
</style>
