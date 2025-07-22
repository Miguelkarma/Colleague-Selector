<template>
  <div class="flex flex-col items-center">
    <p>Hello, My name is {{ name }} and my age is {{ age }}</p>
    <h2>{{ count }}</h2>
    <div class="flex flex-col w-1/2 mt-2">
      <button
        @click="birthday"
        class="p-2 bg-emerald-300 rounded cursor-pointer"
      >
        Click For your birthday
      </button>
      <button
        @click="decrease"
        class="p-2 bg-orange-300 rounded mt-2 cursor-pointer"
      >
        Click to decrease age
      </button>
    </div>
  </div>
</template>
<script setup>
import { ref } from "vue";
const age = ref(21);
const name = "Migo";

const birthday = () => {
  age.value++;
  alert("Happy birthday bish");
};

const decrease = () => {
  age.value--;
  alert("damn");
};
</script>
<style scoped></style>
