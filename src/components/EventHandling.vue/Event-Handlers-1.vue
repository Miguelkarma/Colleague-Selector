<template>
  <h1>This is the count {{ count }}</h1>
  <button
    class="btn w-40 bg-blue-500 text-cyan-700 py-10 rounded cursor-pointer"
    @click="inc"
  >
    Increment
  </button>
  <button
    class="btn w-40 bg-red-500 text-cyan-700 py-10 rounded cursor-pointer"
    @click="dec"
  >
    Decrement
  </button>
</template>
<script setup>
import { ref } from "vue";
const count = ref(0);

const inc = () => {
  count.value++;
};
const dec = () => {
  count.value--;
};
</script>
