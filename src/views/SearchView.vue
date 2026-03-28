<script setup lang="ts">
import { ref, computed, onMounted } from 'vue'
import { useRoute } from 'vue-router'
import products from '../data/products.json'

const route = useRoute()
const searchQuery = ref('')

const filteredItems = computed(() => {
  if (!searchQuery.value) {
    return []
  }
  const query = searchQuery.value.toLowerCase()
  return products.filter(product => 
    product.name.toLowerCase().includes(query) || 
    product.description.toLowerCase().includes(query) || 
    product.category.toLowerCase().includes(query)
  )
})

onMounted(() => {
  const q = route.query.q as string
  if (q) {
    searchQuery.value = q
  }
})

const handleSearch = () => {
  // 搜索逻辑已在计算属性中处理
}
</script>

<template>
  <div class="search-page">
    <div class="container">
      <h1 class="search-title">搜索商品</h1>
      <div class="search-bar">
        <input
          type="text"
          v-model="searchQuery"
          placeholder="输入关键词搜索..."
          class="search-input"
          @keyup.enter="handleSearch"
        />
        <button class="search-button" @click="handleSearch">搜索</button>
      </div>
      
      <div class="search-results">
        <h2 class="results-title">
          {{ searchQuery ? `搜索结果: "${searchQuery}"` : '请输入搜索关键词' }}
        </h2>
        
        <div v-if="filteredItems.length > 0" class="products-grid">
          <div v-for="product in filteredItems" :key="product.id" class="product-card">
            <router-link :to="`/product/${product.id}`" class="product-link">
              <div class="product-image">
                <img :src="product.images[0]" :alt="product.name" />
              </div>
              <div class="product-info">
                <h3 class="product-name">{{ product.name }}</h3>
                <p class="product-description">{{ product.description }}</p>
                <div class="product-price">¥{{ product.price }}</div>
                <div class="product-rating">
                  <span v-for="i in 5" :key="i" class="star">
                    {{ i <= Math.floor(product.rating) ? '★' : '☆' }}
                  </span>
                  <span class="rating-text">{{ product.rating }}</span>
                </div>
              </div>
            </router-link>
          </div>
        </div>
        
        <div v-else-if="searchQuery" class="no-results">
          <p>未找到匹配的商品，请尝试其他关键词</p>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.search-page {
  padding: 60px 0;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
}

.search-title {
  font-size: 32px;
  font-weight: 700;
  text-align: center;
  margin: 0 0 40px;
  color: #333;
}

.search-bar {
  display: flex;
  max-width: 600px;
  margin: 0 auto 40px;
  gap: 10px;
}

.search-input {
  flex: 1;
  padding: 12px 16px;
  border: 1px solid #ddd;
  border-radius: 4px;
  font-size: 16px;
  transition: border-color 0.3s ease;
}

.search-input:focus {
  outline: none;
  border-color: #999;
}

.search-button {
  padding: 12px 24px;
  background-color: #333;
  color: #fff;
  border: none;
  border-radius: 4px;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.search-button:hover {
  background-color: #555;
}

.results-title {
  font-size: 24px;
  font-weight: 600;
  margin: 0 0 30px;
  color: #333;
}

.products-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 40px;
}

.product-card {
  background-color: white;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.product-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.15);
}

.product-link {
  display: block;
  text-decoration: none;
  color: #333;
}

.product-image {
  width: 100%;
  height: 250px;
  overflow: hidden;
}

.product-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.3s ease;
}

.product-card:hover .product-image img {
  transform: scale(1.05);
}

.product-info {
  padding: 20px;
}

.product-name {
  font-size: 18px;
  font-weight: 600;
  margin: 0 0 10px;
}

.product-description {
  font-size: 14px;
  color: #666;
  margin: 0 0 15px;
  line-height: 1.4;
}

.product-price {
  font-size: 20px;
  font-weight: 700;
  color: #333;
  margin: 0 0 10px;
}

.product-rating {
  display: flex;
  align-items: center;
  gap: 5px;
}

.star {
  color: #ffc107;
  font-size: 14px;
}

.rating-text {
  font-size: 14px;
  color: #666;
  margin-left: 5px;
}

.no-results {
  text-align: center;
  padding: 60px 0;
  color: #666;
  font-size: 18px;
}

@media (max-width: 768px) {
  .search-title {
    font-size: 28px;
    margin-bottom: 30px;
  }

  .search-bar {
    flex-direction: column;
  }

  .search-input {
    width: 100%;
  }

  .search-button {
    width: 100%;
  }

  .results-title {
    font-size: 20px;
    margin-bottom: 20px;
  }

  .products-grid {
    grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
    gap: 30px;
  }
}
</style>