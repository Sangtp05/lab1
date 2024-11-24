<!-- App.vue -->
<template>
    <div class="product-carousel">
      <ProductCard
        v-for="(product, index) in products"
        :key="index"
        :product="product"
      />
    </div>
  </template>
  
  <script setup>
  import ProductCard from "./components/ProductCard.vue";
  
  const products = [
    {
      name: "Màn Hình Samsung",
      originalPrice: 500000,
      discount: 50,
      deliveryDate: "05/11",
      rating: 5,
      tags: ["Top Deal", "Freeship Extra"],
      images: [
        "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQLX3y9NBYQN1Fduo2ctnQOtzG2KnDDALOyLA&s",
        "https://stcv4.hnammobile.com/downloads/f/tong-hop-50-hinh-anh-iphone-15-moi-nhat-tren-thi-truong-hien-nay-01699258796.jpg",
        "https://cdn.tgdd.vn/Files/2020/04/09/1247866/untitled-3_800x450.jpg",
      ],
    },
    {
      name: "Adapter Sạc",
      originalPrice: 700000,
      discount: 50,
      deliveryDate: "05/11",
      rating: 4,
      tags: ["Chính hãng", "Freeship Extra"],
      images: [
        "https://macone.vn/wp-content/uploads/2021/12/269902633_648553806568650_2291142193696422643_n-1024x1024.jpeg",
        "https://cdn.tgdd.vn/Products/Images/42/329148/iphone-16-pro-titan-den.png",
        "https://vcdn1-sohoa.vnecdn.net/2022/09/08/DSF6630_1662619594.jpg?w=1200&h=0&q=100&dpr=1&fit=crop&s=6byKEzudsbaLQY5l9kkOlA",
      ],
    },
    {
      name: "ip15",
      originalPrice: 700000,
      discount: 50,
      deliveryDate: "05/11",
      rating: 4,
      tags: ["Chính hãng", "Freeship Extra"],
      images: [
        "https://macone.vn/wp-content/uploads/2021/12/269902633_648553806568650_2291142193696422643_n-1024x1024.jpeg",
        "https://cdn.tgdd.vn/Products/Images/42/329148/iphone-16-pro-titan-den.png",
        "https://vcdn1-sohoa.vnecdn.net/2022/09/08/DSF6630_1662619594.jpg?w=1200&h=0&q=100&dpr=1&fit=crop&s=6byKEzudsbaLQY5l9kkOlA",
      ],
    },
  ];
  </script>
  
  <style scoped>
  .product-carousel {
    display: flex;
    overflow-x: scroll;
  }
  </style> <!-- ProductCard.vue -->
  
  <style scoped>
  .product-card {
    width: 300px;
    margin: auto;
  }
  
  .fixed-image {
    height: 200px;
    object-fit: cover;
    border-radius: 8px;
  }
  
  .current-price {
    color: #dc3545;
    font-weight: bold;
  }
  
  .original-price {
    text-decoration: line-through;
  }
  
  .quantity-input {
    display: flex;
    flex-direction: column;
  }
  
  .quantity-input input {
    width: 100%;
  }
  </style>
  
  <template>
    <div class="product-card card shadow-sm">
      <div id="carouselExample" class="carousel slide" data-bs-ride="carousel">
        <div class="carousel-inner">
          <div
            v-for="(image, index) in product.images"
            :key="index"
            :class="['carousel-item', { active: index === currentImageIndex }]"
            :data-bs-interval="1000"
          >
            <img
              :src="image"
              alt="Product Image"
              class="d-block w-100 fixed-image"
            />
          </div>
        </div>
      </div>
  
      <div class="card-body">
        <h5 class="product-name card-title">{{ product.name }}</h5>
        <div class="rating mb-2">
          <span v-for="n in product.rating" :key="n" class="text-warning"
            >⭐</span
          >
        </div>
        <div class="prices mb-2">
          <span class="current-price me-2">{{ formatCurrency(finalPrice) }}</span>
          <span class="original-price text-muted me-2">{{
            formatCurrency(product.originalPrice)
          }}</span>
          <span class="discount badge bg-success">{{ product.discount }}%</span>
        </div>
        <div class="tags mb-2">
          <span
            v-if="product.tags.includes('Top Deal')"
            class="badge bg-primary me-1"
            >Top Deal</span
          >
          <span
            v-if="product.tags.includes('Chính hãng')"
            class="badge bg-info me-1"
            >Chính hãng</span
          >
          <span
            v-if="product.tags.includes('Freeship Extra')"
            class="badge bg-warning text-dark"
            >Freeship Extra</span
          >
        </div>
        <div class="delivery-date text-muted mb-3">
          Giao thứ {{ product.deliveryDate }}
        </div>
        <div class="quantity-input mb-3">
          <label for="quantity" class="form-label">Số lượng</label>
          <input
            type="number"
            id="quantity"
            v-model="quantity"
            min="1"
            class="form-control"
          />
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref, computed } from "vue";
  
  const props = defineProps({
    product: Object,
  });
  
  const currentImageIndex = ref(0);
  const quantity = ref(1);
  
  const currentPrice = computed(() => {
    return props.product.originalPrice * (1 - props.product.discount / 100);
  });
  
  const finalPrice = computed(() => {
    return currentPrice.value * quantity.value;
  });
  
  function formatCurrency(value) {
    return new Intl.NumberFormat("vi-VN", {
      style: "currency",
      currency: "VND",
    }).format(value);
  }
  </script>