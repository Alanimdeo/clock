<template>
  <p class="digital-clock">
    <span>{{ hour }}</span>
    <span>:</span>
    <span>{{ minute }}</span>
    <span>:</span>
    <span>{{ second }}</span>
    <span>.</span>
    <span>{{ millisecond }}</span>
  </p>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  data() {
    return {
      hour: "00",
      minute: "00",
      second: "00",
      millisecond: "000",
    };
  },
  async mounted() {
    this.updateClock();
  },
  methods: {
    updateClock() {
      setInterval(() => {
        const now = new Date();
        this.hour = getPrettierTime(now.getHours());
        this.minute = getPrettierTime(now.getMinutes());
        this.second = getPrettierTime(now.getSeconds());
        this.millisecond = getPrettierTime(now.getMilliseconds(), 3);
      }, 1);
    },
  },
});

function getPrettierTime(time: number, digits: number = 2) {
  return time.toString().padStart(digits, "0");
}
</script>

<style scoped>
.digital-clock {
  margin: 2rem auto;
  font-size: min(4rem, calc(100vw / 8));
  text-align: center;
}
</style>
