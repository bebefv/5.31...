<template>
  <div id="app">
    <ShoppingCart />
  </div>
</template>

<script>
import ShoppingCart from "@/components/ShoppingCart.vue";

export default {
  name: "App",
  components: {
    ShoppingCart
  }
};
</script>

<style>
#app {
  font-family: Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 60px;
}
</style>
