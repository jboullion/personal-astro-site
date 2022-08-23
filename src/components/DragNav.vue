<script setup lang="ts">
import { ref } from "vue";
import { useDraggable } from "@vueuse/core";

const props = defineProps({
  title: String,
});

const about = ref<HTMLElement | null>(null);
const github = ref<HTMLElement | null>(null);

// `style` will be a helper computed for `left: ?px; top: ?px;`

const { style: aStyle } = useDraggable(about, {
  initialValue: { x: 40, y: 40 },
});
const { style: gStyle } = useDraggable(github, {
  initialValue: { x: 100, y: 40 },
});
</script>
<template>
  <div id="nav">
    <h1>{{ title }}</h1>
    <nav id="contact">
      <a href="/about" ref="about" :style="aStyle" style="position: fixed">?</a>
      <a
        href="https://github.com/jboullion"
        ref="github"
        :style="gStyle"
        style="position: fixed"
        >G</a
      >
    </nav>
  </div>
</template>

<style>
#nav {
  display: flex;
  justify-content: center;
  align-items: center;
}

#nav a {
  color: #fff;
  text-decoration: none;
  font-size: 1.4rem;
  line-height: 1;
  width: 1.4rem;
  text-align: center;
  font-weight: bold;
  transition: color 0.2s ease-in-out;
  margin: 1rem;
  padding: 1rem;
  border: 2px solid white;
  border-radius: 50%;
}
.drag-nav {
  border: 2px solid #ccc;
  background-color: #fff;
  color: black;
  padding: 20px;
  border-radius: 20px;
}
</style>
