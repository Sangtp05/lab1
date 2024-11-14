<script setup lang="ts">
import { Swiper, SwiperSlide } from 'swiper/vue';
import 'swiper/css';

defineProps({
  item: {
    type: Object,
    required: true
  }
});
</script>

<template>
  <div class="product-card">
    <div class="product-image">
      <swiper :slides-per-view="1" :space-between="10">
        <swiper-slide v-for="image in item.images" :key="image.id">
          <img :src="image.url" :alt="item.name" />
        </swiper-slide>
      </swiper>
    </div>
    <div class="product-info">
      <div class="product-tags">
        <img v-for="tag in item.tag" :key="tag.id" :src="tag.url" :alt="tag.name" />
      </div>
      <h3 class="product-name">{{ item.name }}</h3>
      <div class="product-rating">
        <span v-for="n in item.rate" :key="n" class="rating-star">&#9733;</span>
      </div>
      <div class="product-price">
        <span class="price">{{ item.price.toLocaleString() }} VND</span>
        <span class="original-price">{{ item.original_price.toLocaleString() }} VND</span>
        <span class="discount">{{ item.discount }}</span>
      </div>
      <div class="product-delivery">
        <span>Delivery: {{ item.time_delivery }}</span>
      </div>
    </div>
  </div>
</template>

<style scoped>
.product-card {
  display: flex;
  flex-direction: column;
  border: 1px solid #ccc;
  border-radius: 8px;
  overflow: hidden;
}

.product-image {
  height: 300px;
}

.product-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.product-info {
  padding: 16px;
}

.product-tags {
  display: flex;
  margin-bottom: 8px;
}

.product-tags img {
  width: 32px;
  height: 32px;
  margin-right: 8px;
}

.product-name {
  margin-top: 0;
}

.product-rating .rating-star {
  color: #ffc107;
}

.product-price {
  display: flex;
  align-items: center;
  margin-bottom: 8px;
}

.product-price .price {
  font-size: 18px;
  font-weight: bold;
  margin-right: 8px;
}

.product-price .original-price {
  text-decoration: line-through;
  color: #888;
  margin-right: 8px;
}

.product-price .discount {
  background-color: #ff6b6b;
  color: #fff;
  padding: 4px 8px;
  border-radius: 4px;
}

.product-delivery {
  color: #888;
}
</style>
