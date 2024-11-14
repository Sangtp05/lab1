<script setup lang="ts">
import { ref } from 'vue';
import ProductCard from './components/ProductCard.vue';
import dataProduct from './dataSample.js';
</script>

<template>
  <div class="app-container">
    <div class="product-grid">
      <div class="product-item" v-for="item in dataProduct" :key="item.id">
        <ProductCard :item="item" />
      </div>
    </div>
  </div>
</template>

<style scoped>
.app-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
  width: 100vw;
}

.product-grid {
  display: flex;
  width: 100%;
}

.product-item {
  display: flex;
  justify-content: center;
  width: 25%;
}
</style>