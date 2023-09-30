<script setup>
import { RouterLink, RouterView } from "vue-router";
import ProductDisplay from "./components/ProductDisplay.vue";
</script>

<template>
  <ProductDisplay />
</template>

<script>
export default {
  components: {
    ProductDisplay,
  },
};
</script>
