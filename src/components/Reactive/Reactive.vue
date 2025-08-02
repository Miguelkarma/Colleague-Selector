<template>
  <h1>Hello my name is {{ user.name }} and I am {{ user.age }} years old</h1>
  <div class="flex flex-col items-center py-5">
    <form @submit.prevent class="flex flex-col items-center gap-5">
      <input
        v-model="user.name"
        type="text"
        placeholder="enter your name"
        class="rounded border p-2"
      />
      <input
        v-model="user.age"
        type="text"
        placeholder="age"
        class="rounded border p-2"
      />
    </form>
  </div>
</template>
<script setup>
import { reactive } from "vue";

const user = reactive({
  name: "Lawson",
  age: 0,
});
</script>
