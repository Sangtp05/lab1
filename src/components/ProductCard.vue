<!-- ProductCard.vue -->
<template>
  <div class="product-card">
    <div class="product-image">
      <!-- Hiển thị ảnh sản phẩm -->
      <img src="https://via.placeholder.com/150" alt="Product Image">
    </div>
    <div class="product-info">
      <h3 class="product-name">{{ item.name }}</h3>
      <div class="product-price">
        <span class="price">{{ formatPrice(item.price) }}</span>
        <span class="promotion" v-if="item.promotion > 0">-{{ item.promotion }}%</span>
      </div>
      <div class="product-rating">
        <div class="stars">
          <!-- Hiển thị số sao đánh giá -->
          <i class="fas fa-star" v-for="i in item.rate" :key="i"></i>
        </div>
        <span class="reviews">{{ item.rate }} reviews</span>
      </div>
      <div class="product-tags">
        <span class="tag" v-for="tag in item.tag" :key="tag">{{ tag }}</span>
      </div>
      <button class="add-to-cart">Add to Cart</button>
    </div>
  </div>
</template>

<script setup lang="ts">
import { defineProps } from 'vue'

interface ProductItem {
  id: number
  name: string
  promotion: number
  price: number
  rate: number
  tag: string[]
}

defineProps<{
  item: ProductItem
}>()

const formatPrice = (price: number) => {
  return price.toLocaleString('vi-VN', { style: 'currency', currency: 'VND' })
}
</script>

<style scoped>
.product-card {
  display: flex;
  border: 1px solid #ccc;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.product-image {
  flex-basis: 150px;
  overflow: hidden;
}

.product-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.product-info {
  flex-grow: 1;
  padding: 16px;
}

.product-name {
  font-size: 18px;
  font-weight: bold;
  margin-bottom: 8px;
}

.product-price {
  display: flex;
  align-items: center;
  margin-bottom: 8px;
}

.price {
  font-size: 16px;
  font-weight: bold;
  margin-right: 8px;
}

.promotion {
  background-color: #f44336;
  color: #fff;
  padding: 4px 8px;
  border-radius: 4px;
  font-size: 14px;
}

.product-rating {
  display: flex;
  align-items: center;
  margin-bottom: 8px;
}

.stars {
  color: #ffa500;
  margin-right: 8px;
}

.reviews {
  font-size: 14px;
  color: #666;
}

.product-tags {
  display: flex;
  flex-wrap: wrap;
  margin-bottom: 16px;
}

.tag {
  background-color: #f5f5f5;
  color: #333;
  padding: 4px 8px;
  border-radius: 4px;
  font-size: 14px;
  margin-right: 8px;
  margin-bottom: 8px;
}

.add-to-cart {
  background-color: #4CAF50;
  color: #fff;
  border: none;
  padding: 8px 16px;
  border-radius: 4px;
  cursor: pointer;
  font-size: 16px;
}
</style>