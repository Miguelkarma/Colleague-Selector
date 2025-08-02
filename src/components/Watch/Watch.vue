<template>
  <div>
    <h1>You're {{ age }}</h1>
    <h1>{{ display }}</h1>
    <input
      v-model.number="age"
      type="text"
      placeholder="update age"
      class="rounded border p-2"
    />
  </div>
</template>
<script setup>
import { ref, watch } from "vue";

const age = ref(21);
const display = ref("");

watch(age, (newAge, oldAge) => {
  display.value = `Age changed from ${oldAge} to ${newAge}`;
});
</script>
