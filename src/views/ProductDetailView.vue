<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { useRoute, useRouter } from 'vue-router'
import products from '../data/products.json'

const route = useRoute()
const router = useRouter()
const product = ref<any>(null)
const loading = ref(true)
const selectedSize = ref<any>(null)
const currentImageIndex = ref(0)

onMounted(() => {
  const id = parseInt(route.params.id as string)
  const foundProduct = products.find(p => p.id === id)
  if (foundProduct) {
    product.value = foundProduct
    selectedSize.value = foundProduct.sizes[0]
  } else {
    // 商品不存在，重定向到首页
    router.push('/')
  }
  loading.value = false
})

const handleSizeChange = (size: any) => {
  selectedSize.value = size
}

const nextImage = () => {
  if (product.value) {
    currentImageIndex.value = (currentImageIndex.value + 1) % product.value.images.length
  }
}

const prevImage = () => {
  if (product.value) {
    currentImageIndex.value = (currentImageIndex.value - 1 + product.value.images.length) % product.value.images.length
  }
}

const selectImage = (index: number) => {
  currentImageIndex.value = index
}
</script>

<template>
  <div class="product-detail">
    <div class="container">
      <div v-if="loading" class="loading">加载中...</div>
      <div v-else-if="product" class="product-content">
        <div class="product-image-section">
          <div class="image-carousel">
            <div class="main-image-container">
              <img :src="product.images[currentImageIndex]" :alt="product.name" class="main-image" />
              <button class="carousel-btn prev" @click="prevImage">&lt;</button>
              <button class="carousel-btn next" @click="nextImage">&gt;</button>
            </div>
            <div class="thumbnail-container">
              <div
                v-for="(image, index) in product.images"
                :key="index"
                class="thumbnail-item"
                :class="{ active: index === currentImageIndex }"
                @click="selectImage(Number(index))"
              >
                <img :src="image" :alt="`${product.name} - View ${Number(index) + 1}`" class="thumbnail-image" />
              </div>
            </div>
          </div>
        </div>
        <div class="product-info-section">
          <h1 class="product-title">{{ product.name }}</h1>
          <div class="product-category">{{ product.category }}</div>
          <div class="product-model">型号ID: {{ product.modelId }}</div>
          <div class="product-rating">
            <span v-for="i in 5" :key="i" class="star">
              {{ i <= Math.floor(product.rating) ? '★' : '☆' }}
            </span>
            <span class="rating-text">{{ product.rating }}</span>
          </div>
          <div class="product-price">¥{{ selectedSize.price }}</div>
          
          <!-- 尺寸选择选项卡 -->
          <div class="size-selection">
            <h3 class="size-title">选择尺寸</h3>
            <div class="size-options">
              <button
                v-for="size in product.sizes"
                :key="size.size"
                class="size-option"
                :class="{ active: selectedSize.size === size.size }"
                @click="handleSizeChange(size)"
              >
                {{ size.size }}
                <span class="size-price">¥{{ size.price }}</span>
              </button>
            </div>
          </div>
          
          <div class="product-description">
            <h2 class="description-title">商品描述</h2>
            <p>{{ product.description }}</p>
          </div>
          <div class="product-actions">
            <button class="action-button primary">加入购物车</button>
            <button class="action-button secondary">收藏</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.product-detail {
  padding: 60px 0;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
}

.loading {
  text-align: center;
  padding: 100px 0;
  font-size: 18px;
  color: #666;
}

.product-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 60px;
  align-items: start;
}

.product-image-section {
  background-color: #f8f8f8;
  border-radius: 8px;
  overflow: hidden;
  padding: 40px;
}

.image-carousel {
  width: 100%;
}

.main-image-container {
  position: relative;
  width: 100%;
  height: 500px;
  overflow: hidden;
  margin-bottom: 20px;
  border-radius: 4px;
}

.main-image {
  width: 100%;
  height: 100%;
  object-fit: contain;
}

.carousel-btn {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background-color: rgba(255, 255, 255, 0.7);
  color: #333;
  border: none;
  border-radius: 50%;
  width: 40px;
  height: 40px;
  font-size: 20px;
  cursor: pointer;
  transition: background-color 0.3s ease;
  z-index: 10;
}

.carousel-btn:hover {
  background-color: rgba(255, 255, 255, 0.9);
}

.carousel-btn.prev {
  left: 20px;
}

.carousel-btn.next {
  right: 20px;
}

.thumbnail-container {
  display: flex;
  gap: 10px;
  overflow-x: auto;
  padding-bottom: 10px;
}

.thumbnail-item {
  flex: 0 0 auto;
  width: 100px;
  height: 100px;
  border-radius: 4px;
  overflow: hidden;
  cursor: pointer;
  border: 2px solid transparent;
  transition: all 0.3s ease;
}

.thumbnail-item:hover {
  border-color: #333;
  transform: scale(1.05);
}

.thumbnail-item.active {
  border-color: #333;
  box-shadow: 0 0 0 2px #fff, 0 0 0 4px #333;
}

.thumbnail-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

/* 响应式设计 */
@media (max-width: 768px) {
  .main-image-container {
    height: 300px;
  }

  .carousel-btn {
    width: 30px;
    height: 30px;
    font-size: 16px;
  }

  .thumbnail-item {
    width: 80px;
    height: 80px;
  }
}

@media (max-width: 480px) {
  .main-image-container {
    height: 250px;
  }

  .thumbnail-item {
    width: 60px;
    height: 60px;
  }
}

.product-info-section {
  padding: 20px 0;
}

.product-title {
  font-size: 32px;
  font-weight: 700;
  margin: 0 0 15px;
  color: #333;
}

.product-category {
  font-size: 14px;
  color: #666;
  margin: 0 0 15px;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.product-model {
  font-size: 14px;
  color: #666;
  margin: 0 0 15px;
}

.product-rating {
  display: flex;
  align-items: center;
  gap: 5px;
  margin: 0 0 20px;
}

.star {
  color: #ffc107;
  font-size: 16px;
}

.rating-text {
  font-size: 16px;
  color: #666;
  margin-left: 10px;
}

.product-price {
  font-size: 36px;
  font-weight: 700;
  color: #333;
  margin: 0 0 30px;
}

.description-title {
  font-size: 20px;
  font-weight: 600;
  margin: 0 0 15px;
  color: #333;
}

.product-description {
  margin: 0 0 40px;
}

.product-description p {
  font-size: 16px;
  line-height: 1.6;
  color: #666;
  margin: 0;
}

/* 尺寸选择样式 */
.size-selection {
  margin: 30px 0;
}

.size-title {
  font-size: 18px;
  font-weight: 600;
  margin: 0 0 15px;
  color: #333;
}

.size-options {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
}

.size-option {
  padding: 10px 20px;
  border: 1px solid #ddd;
  border-radius: 4px;
  background-color: white;
  font-size: 14px;
  cursor: pointer;
  transition: all 0.3s ease;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 5px;
  min-width: 100px;
}

.size-option:hover {
  border-color: #333;
  transform: translateY(-2px);
}

.size-option.active {
  border-color: #333;
  background-color: #f8f8f8;
  font-weight: 600;
}

.size-price {
  font-size: 12px;
  color: #666;
}

.size-option.active .size-price {
  color: #333;
  font-weight: 500;
}

.product-actions {
  display: flex;
  gap: 20px;
}

.action-button {
  padding: 15px 30px;
  border: none;
  border-radius: 4px;
  font-size: 16px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
  flex: 1;
}

.action-button.primary {
  background-color: #333;
  color: #fff;
}

.action-button.primary:hover {
  background-color: #555;
  transform: translateY(-2px);
}

.action-button.secondary {
  background-color: #f8f8f8;
  color: #333;
  border: 1px solid #ddd;
}

.action-button.secondary:hover {
  background-color: #f0f0f0;
  transform: translateY(-2px);
}

@media (max-width: 768px) {
  .product-content {
    grid-template-columns: 1fr;
    gap: 40px;
  }

  .product-image-section {
    padding: 20px;
  }

  .product-title {
    font-size: 28px;
  }

  .product-price {
    font-size: 32px;
  }

  .product-actions {
    flex-direction: column;
  }

  .action-button {
    width: 100%;
  }
}
</style>