<template>
  <div class="mx-auto">
    <div class="flex flex-col items-center justify-center gap-3">
      <a :href="randomLink">welcome to my domain</a>
      <img v-bind="desc" />

      <Events />
    </div>
  </div>
</template>
<script setup>
import Events from "@/components/EventHandles.vue";
const randomLink =
  "https://www.reddit.com/r/learnprogramming/comments/v8gtq0/selftaught_developers_how_much_did_you_know_when/";

const desc = {
  src: new URL("./assets/pic.jpg", import.meta.url).href,
  alt: "Hooman",
  width: 200,
  height: 300,
};
</script>
