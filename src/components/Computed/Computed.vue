<template>
  <div>
    <h1>{{ nameCheck }}</h1>
    <input
      type="text"
      v-model="name"
      placeholder="Enter your name"
      class="rounded border p-2"
    />
  </div>
</template>
<script setup>
import { computed, ref } from "vue";

const name = ref("");

const nameCheck = computed(() => {
  return name.value.trim().length < 5 ? "Name is too short" : "name is valid g";
});
</script>
