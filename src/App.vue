<template>
  <div class="clock" @click="fullscreenToggle()">
    <AnalogClock />
    <DigitalClock />
  </div>
</template>

<script setup lang="ts">
import AnalogClock from "./components/AnalogClock.vue";
import DigitalClock from "./components/DigitalClock.vue";

function fullscreenToggle() {
  const doc = document.documentElement;
  if (!document.fullscreenElement) {
    doc.requestFullscreen().catch((err) => {
      alert(`Error attempting to enable full-screen mode: ${err.message} (${err.name})`);
    });
  } else {
    if (document.exitFullscreen) {
      document.exitFullscreen();
    }
  }
}
</script>

<style scoped>
.clock {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  width: 100vw;
  height: 100vh;
}
</style>

<style>
@import url("https://fonts.googleapis.com/css2?family=Overpass+Mono:wght@700&display=swap");
body {
  margin: 0;
  font-family: "Overpass Mono", monospace;
  font-weight: 600;
}
</style>
