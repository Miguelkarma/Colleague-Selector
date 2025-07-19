<template>
  <div class="m-auto bg-white p-4 rounded shadow-md max-w-md mt-2">
    <h1>{{ msg }}</h1>
    <p>Using text interpolation: {{ rawHtml }}</p>
    <p>Using v-html directive: <span v-html="rawHtml"></span></p>
  </div>
  <div>
    <div class="mx-auto">
      <h1 :id="dynamicId" class="text-center mt-2">
        A wild Pokemon has appeared
      </h1>
    </div>
    <img
      class="mx-auto mt-4 p-4 bg-gray-400 rounded shadow-md"
      :src="imageURL"
      alt="vuelogo"
    />
  </div>
</template>

<script>
import logoImage from "@/assets/pic.jpg";
export default {
  data() {
    return {
      imageURL: logoImage,
      msg: "sup dawg",
      rawHtml: "<strong>this is raw dog</strong>",
      dynamicId: "section-123",
    };
  },
};
</script>
