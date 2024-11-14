<script setup lang="ts">
import ProductCard from './components/ProductCard.vue';
const listProducts = [{
  id: 1,
  image: "",
  name: "product 1",
  promotion: 20,
  price: 40000,
  rate: 5,
  tag: ["123", "123", "123"]
}, {
  id: 2,
  image: "",
  name: "product 2",
  promotion: 40,
  price: 40000,
  rate: 5,
  tag: ["123", "123", "123"],
  
}]
</script>
<template>
  <div v-for="item in listProducts">
    <ProductCard msg="Vite + Vue" :item="item" />
  </div>
</template>
