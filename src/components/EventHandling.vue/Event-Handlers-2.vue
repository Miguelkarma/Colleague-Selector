<template>
  <div class="mx-auto">
    <div class="flex flex-col items-center py-5">
      <form @:submit="submitHandler" class="flex flex-col items-center gap-5">
        <input
          type="text"
          placeholder="enter your name"
          class="rounded border p-2"
        />
        <input
          type="text"
          placeholder="enter your email"
          class="rounded border p-2"
        />
        <button
          class="btn w-40 bg-red-500 text-cyan-700 py-10 rounded cursor-pointer"
        >
          submit
        </button>
      </form>
      <h1 class="items-center">ref</h1>
      <button
        @click="toggle"
        class="btn w-40 bg-red-500 text-cyan-700 py-10 rounded cursor-pointer mt-10"
      >
        Click to appear paragraph lol
      </button>
      <p v-if="isVisible">hehe</p>
    </div>
    <div class="mx-auto flex justify-center">
      <h1 class="items-center">Reactive</h1>
    </div>
  </div>
</template>
<script setup>
import { reactive, ref } from "vue";
const isVisible = ref(false);

const toggle = () => {
  isVisible.value = !isVisible.value;
};
const submitHandler = (e) => {
  e.preventDefault();
  alert("Creds Valid");
};
</script>
