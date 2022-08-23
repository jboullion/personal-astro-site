<script setup lang="ts">
import { onMounted, ref } from "vue";

let startPosition = [0, 0];
const moving = ref(true);
const loaded = ref(false);

let stars: HTMLElement | null = null;
let stars2: HTMLElement | null = null;
let stars3: HTMLElement | null = null;

onMounted(() => {
  stars = document.getElementById("stars");
  stars2 = document.getElementById("stars2");
  stars3 = document.getElementById("stars3");

  loaded.value = true;
});

function startMove(e: MouseEvent) {
  //moving.value = !moving.value;
  startPosition = [e.clientX, e.clientY];
}

function moveStars(e: MouseEvent) {
  if (!moving.value || !stars || !stars2 || !stars3) return;

  const newPosition = [
    startPosition[0] - e.clientX,
    startPosition[1] - e.clientY,
  ];

  // TODO: Possibly setup a lastPosition to we can move stars relative to the last position instead of always the start position.
  // TODO: Possibly use VueUse library to track mouse?

  stars.style.backgroundPositionX = newPosition[0] + "px";
  stars.style.backgroundPositionY = newPosition[1] + "px";
  stars2.style.backgroundPositionX = newPosition[0] / 2 + "px";
  stars2.style.backgroundPositionY = newPosition[1] / 2 + "px";
  stars3.style.backgroundPositionX = newPosition[0] / 4 + "px";
  stars3.style.backgroundPositionY = newPosition[1] / 4 + "px";
}
</script>
<template>
  <div
    class="stars"
    :class="{ loaded: loaded }"
    @click="startMove"
    @mousemove="moveStars"
    style="opacity: 0"
  >
    <div id="stars" class="stars"></div>
    <div id="stars2" class="stars"></div>
    <div id="stars3" class="stars"></div>
  </div>
</template>

<style>
.stars {
  position: fixed;
  top: 0;
  bottom: 0;
  width: 100%;
  background-attachment: fixed;
  background-size: 100% 100%;
  background-position: 0px 0px;

  transition: opacity 1.5s ease-in;
}

.stars.loaded {
  opacity: 1 !important;
}

#stars {
  background-image: url("/assets/stars1.png");
}

#stars2 {
  background-image: url("/assets/stars2.png");
}

#stars3 {
  background-image: url("/assets/stars3.png");
}
</style>
