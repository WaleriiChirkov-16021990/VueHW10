<template>
  <div id="app">
    <ProductList></ProductList>
  </div>
</template>

<script>

import ProductList from "@/components/ProductList.vue";

export default {
  name: 'App',
  components: {
    ProductList
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  max-width: 1920px;
  width: 100%;
}
</style>
