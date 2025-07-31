<template>
  <h1>This is the count {{ count }}</h1>
  <button
    class="btn w-40 bg-blue-500 text-cyan-700 py-10 rounded"
    @click="count++"
  >
    Increment
  </button>
  <button
    class="btn w-40 bg-red-500 text-cyan-700 py-10 rounded"
    @click="count--"
  >
    Decrement
  </button>
</template>
<script setup>
import { ref } from "vue";
const count = ref(0);
</script>
