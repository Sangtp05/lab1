<template>
  <div class="product-card">
    <!-- Slider Hình Ảnh -->
    <div class="image-slider">
      <img :src="images[currentImage]" alt="Product Image" class="product-image" />
    </div>

    <!-- Tags -->
    <div class="tags">
      <span v-if="isTopDeal" class="tag top-deal">Top Deal</span>
      <span v-if="isOfficial" class="tag official">Chính hãng</span>
      <span v-if="hasFreeShipping" class="tag free-shipping">Freeship Extra</span>
    </div>

    <!-- Thông tin sản phẩm -->
    <h3 class="product-name">{{ productName }}</h3>
    <div class="rating">
      <span v-for="n in 5" :key="n" class="star" :class="{ active: n <= rating }">★</span>
    </div>

    <div class="price-section">
      <p class="current-price">{{ currentPrice.toLocaleString() }}₫</p>
      <p class="original-price">{{ originalPrice.toLocaleString() }}₫</p>
      <p class="discount">-{{ discountPercentage }}%</p>
    </div>

    <p class="delivery-date">Giao từ: {{ estimatedDelivery }}</p>
  </div>
</template>

<script>
export default {
  name: "ProductCard",
  props: {
    images: {
      type: Array,
      default: () => [
        "https://curnonwatch.com/blog/wp-content/uploads/2021/03/anh-dong-ho-dep-55-1536x864.jpg",
        "https://curnonwatch.com/blog/wp-content/uploads/2021/03/anh-dong-ho-dep-62-1536x864.jpg",
        "https://curnonwatch.com/blog/wp-content/uploads/2021/03/anh-dong-ho-dep-58-1536x864.jpg"
      ]
    },
    productName: {
      type: String,
      default: "Đồng hồ vip"
    },
    rating: {
      type: Number,
      default: 4
    },
    currentPrice: {
      type: Number,
      default: 999999
    },
    originalPrice: {
      type: Number,
      default: 1999999
    },
    discountPercentage: {
      type: Number,
      default: 20
    },
    deliveryDays: {
      type: Number,
      default: 5
    },
    isTopDeal: {
      type: Boolean,
      default: true
    },
    isOfficial: {
      type: Boolean,
      default: true
    },
    hasFreeShipping: {
      type: Boolean,
      default: true
    }
  },
  data() {
    return {
      currentImage: 0,
      estimatedDelivery: ""
    };
  },
  mounted() {
    this.startImageSlider();
    this.calculateDeliveryDate();
  },
  methods: {
    startImageSlider() {
      setInterval(() => {
        this.currentImage = (this.currentImage + 1) % this.images.length;
      }, 2000);
    },
    calculateDeliveryDate() {
      const currentDate = new Date();
      currentDate.setDate(currentDate.getDate() + this.deliveryDays);
      this.estimatedDelivery = currentDate.toLocaleDateString("vi-VN");
    }
  }
};
</script>

<style>
.product-card {
  width: 180px;
  border: 2px solid #00FF00; /* Green border */
  border-radius: 10px;
  padding: 8px; /* Reduced padding */
  background-color: #ffffff;
  text-align: center;
  font-family: Arial, sans-serif;
}

.image-slider {
  width: 100%;
  overflow: hidden;
}

.product-image {
  width: 100%;
  border-radius: 5px;
} .tags {
  display: flex;
  justify-content: center;
  gap: 3px; /* Reduced gap */
  margin-top: 3px; /* Reduced margin */
}

.tag {
  font-size: 10px;
  padding: 2px 4px;
  border-radius: 3px;
  color: #ffffff;
}

.top-deal {
  background-color: #ff0000; /* Red background */
}

.official {
  background-color: #007bff; /* Blue background */
}

.free-shipping {
  background-color: #ff7f50; /* Coral background */
}

.product-name {
  font-size: 14px;
  font-weight: bold;
  color: #333333;
  margin: 4px 0; /* Tighter margin */
}

.rating {
  margin: 2px 0; /* Tighter spacing around stars */
}

.rating .star {
  font-size: 12px;
  color: #FFD700; /* Gold color */
}

.rating .star.active {
  color: #FFD700; /* Active stars in gold */
}

.price-section {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 2px; /* Reduced margin */
}

.current-price {
  font-size: 16px;
  font-weight: bold;
  color: #ff0000; /* Red color */
  margin: 2px 0; /* Tighter spacing */
}

.original-price {
  font-size: 12px;
  text-decoration: line-through;
  color: #999999;
  margin: 1px 0; /* Tighter spacing */
}

.discount {
  font-size: 12px;
  color: #ff0000; /* Red color */
  margin: 1px 0; /* Tighter spacing */
}

.delivery-date {
  font-size: 12px;
  color: #999999;
  margin-top: 4px; /* Tighter margin */
}

</style>​