<script setup lang="ts">
import { ref, onMounted } from 'vue'
import products from '../data/products.json'

const currentSlide = ref(0)
const slides = [
  {
    id: 1,
    image: 'https://trae-api-cn.mchost.guru/api/ide/v1/text_to_image?prompt=minimalist%20home%20interior%20with%20modern%20furniture%2C%20clean%20lines%2C%20bright%20space&image_size=landscape_16_9',
    title: 'Minimalist Home Style',
    description: 'Explore a simple yet sophisticated lifestyle'
  },
  {
    id: 2,
    image: 'https://trae-api-cn.mchost.guru/api/ide/v1/text_to_image?prompt=modern%20living%20room%20with%20minimalist%20design%2C%20neutral%20colors%2C%20natural%20light&image_size=landscape_16_9',
    title: 'Modern Living Space',
    description: 'Create a comfortable and stylish living environment'
  },
  {
    id: 3,
    image: 'https://trae-api-cn.mchost.guru/api/ide/v1/text_to_image?prompt=minimalist%20bedroom%20with%20clean%20design%2C%20soft%20colors%2C%20functional%20furniture&image_size=landscape_16_9',
    title: 'Tranquil Bedroom',
    description: 'Create a peaceful and comfortable resting space'
  }
]

const categories = [
  {
    id: 1,
    name: 'Furniture',
    image: 'https://trae-api-cn.mchost.guru/api/ide/v1/text_to_image?prompt=minimalist%20furniture%20collection%2C%20modern%20design&image_size=landscape_16_9',
    count: 12
  },
  {
    id: 2,
    name: 'Lighting',
    image: 'https://trae-api-cn.mchost.guru/api/ide/v1/text_to_image?prompt=modern%20minimalist%20lighting%20fixtures&image_size=landscape_16_9',
    count: 8
  },
  {
    id: 3,
    name: 'Home Decor',
    image: 'https://trae-api-cn.mchost.guru/api/ide/v1/text_to_image?prompt=minimalist%20home%20decor%20items&image_size=landscape_16_9',
    count: 15
  },
  {
    id: 4,
    name: 'Storage',
    image: 'https://trae-api-cn.mchost.guru/api/ide/v1/text_to_image?prompt=minimalist%20storage%20solutions&image_size=landscape_16_9',
    count: 10
  }
]

const testimonials = [
  {
    id: 1,
    name: 'Emma Johnson',
    avatar: 'https://trae-api-cn.mchost.guru/api/ide/v1/text_to_image?prompt=professional%20woman%20portrait%2C%20minimalist%20style&image_size=square',
    comment: 'The quality of the furniture is exceptional. It perfectly fits our minimalist home decor.',
    rating: 5
  },
  {
    id: 2,
    name: 'Michael Chen',
    avatar: 'https://trae-api-cn.mchost.guru/api/ide/v1/text_to_image?prompt=professional%20man%20portrait%2C%20minimalist%20style&image_size=square',
    comment: 'I love the clean design and functionality of every piece I purchased.',
    rating: 4
  },
  {
    id: 3,
    name: 'Sophia Williams',
    avatar: 'https://trae-api-cn.mchost.guru/api/ide/v1/text_to_image?prompt=young%20woman%20portrait%2C%20minimalist%20style&image_size=square',
    comment: 'The delivery was prompt and the assembly was straightforward. Highly recommended!',
    rating: 5
  }
]

const featuredProducts = ref(products.slice(0, 4))

const nextSlide = () => {
  currentSlide.value = (currentSlide.value + 1) % slides.length
}

const prevSlide = () => {
  currentSlide.value = (currentSlide.value - 1 + slides.length) % slides.length
}

onMounted(() => {
  setInterval(nextSlide, 5000)
})
</script>

<template>
  <div class="home">
    <!-- 轮播图 -->
    <div class="carousel">
      <div class="carousel-container">
        <div
          v-for="(slide, index) in slides"
          :key="slide.id"
          class="carousel-slide"
          :class="{ active: index === currentSlide }"
        >
          <img :src="slide.image" :alt="slide.title" class="carousel-image" />
          <div class="carousel-content">
            <h2 class="carousel-title">{{ slide.title }}</h2>
            <p class="carousel-description">{{ slide.description }}</p>
          </div>
        </div>
      </div>
      <button class="carousel-btn prev" @click="prevSlide">&lt;</button>
      <button class="carousel-btn next" @click="nextSlide">&gt;</button>
      <div class="carousel-indicators">
        <button
          v-for="(slide, index) in slides"
          :key="slide.id"
          class="carousel-indicator"
          :class="{ active: index === currentSlide }"
          @click="currentSlide = index"
        ></button>
      </div>
    </div>

    <!-- 商品展示 -->
    <div class="products-section">
      <div class="container">
        <h2 class="section-title">Featured Products</h2>
        <div class="products-grid">
          <div v-for="product in products" :key="product.id" class="product-card">
            <router-link :to="`/product/${product.id}`" class="product-link">
              <div class="product-image">
                <img :src="product.images[0]" :alt="product.name" />
              </div>
              <div class="product-info">
                <h3 class="product-name">{{ product.name }}</h3>
                <div class="product-model">Model: {{ product.modelId }}</div>
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
      </div>
    </div>

    <!-- 分类导航 -->
    <div class="categories-section">
      <div class="container">
        <h2 class="section-title">Shop by Category</h2>
        <div class="categories-grid">
          <div v-for="category in categories" :key="category.id" class="category-card">
            <div class="category-image">
              <img :src="category.image" :alt="category.name" />
            </div>
            <div class="category-content">
              <h3 class="category-name">{{ category.name }}</h3>
              <p class="category-count">{{ category.count }} Products</p>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- 品牌理念 -->
    <div class="brand-section">
      <div class="container">
        <div class="brand-content">
          <div class="brand-text">
            <h2 class="section-title">Our Brand Philosophy</h2>
            <p class="brand-description">
              At Minimal Home, we believe that less is more. Our design philosophy focuses on creating functional, 
              aesthetically pleasing products that enhance your living space without unnecessary clutter. 
              We carefully select materials and craftsmanship to ensure each piece meets our high standards of quality and durability.
            </p>
            <router-link to="/about" class="brand-link">Learn More</router-link>
          </div>
          <div class="brand-image">
            <img src="https://trae-api-cn.mchost.guru/api/ide/v1/text_to_image?prompt=minimalist%20brand%20philosophy%20visual%2C%20clean%20design%2C%20modern%20aesthetic&image_size=landscape_16_9" alt="Brand Philosophy" />
          </div>
        </div>
      </div>
    </div>

    <!-- 客户评价 -->
    <div class="testimonials-section">
      <div class="container">
        <h2 class="section-title">Customer Reviews</h2>
        <div class="testimonials-grid">
          <div v-for="testimonial in testimonials" :key="testimonial.id" class="testimonial-card">
            <div class="testimonial-avatar">
              <img :src="testimonial.avatar" :alt="testimonial.name" />
            </div>
            <div class="testimonial-content">
              <div class="testimonial-rating">
                <span v-for="i in 5" :key="i" class="star">
                  {{ i <= testimonial.rating ? '★' : '☆' }}
                </span>
              </div>
              <p class="testimonial-comment">{{ testimonial.comment }}</p>
              <h4 class="testimonial-name">{{ testimonial.name }}</h4>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- 特色商品 -->
    <div class="featured-section">
      <div class="container">
        <h2 class="section-title">Editor's Picks</h2>
        <div class="products-grid">
          <div v-for="product in featuredProducts" :key="product.id" class="product-card">
            <router-link :to="`/product/${product.id}`" class="product-link">
              <div class="product-image">
                <img :src="product.images[0]" :alt="product.name" />
                <div class="featured-badge">Editor's Pick</div>
              </div>
              <div class="product-info">
                <h3 class="product-name">{{ product.name }}</h3>
                <div class="product-model">Model: {{ product.modelId }}</div>
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
      </div>
    </div>

    <!-- 促销模块 -->
    <div class="promotion-section">
      <div class="container">
        <div class="promotion-content">
          <div class="promotion-text">
            <h2 class="promotion-title">Free Shipping on Orders Over ¥1000</h2>
            <p class="promotion-description">Shop now and enjoy free shipping on all orders over ¥1000. Limited time offer!</p>
            <router-link to="/search" class="promotion-link">Shop Now</router-link>
          </div>
          <div class="promotion-image">
            <img src="https://trae-api-cn.mchost.guru/api/ide/v1/text_to_image?prompt=minimalist%20promotion%20banner%2C%20clean%20design%2C%20modern%20aesthetic&image_size=landscape_16_9" alt="Promotion" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.home {
  width: 100%;
}

/* 轮播图样式 */
.carousel {
  position: relative;
  width: 100%;
  height: 600px;
  overflow: hidden;
}

.carousel-container {
  position: relative;
  width: 100%;
  height: 100%;
}

.carousel-slide {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  opacity: 0;
  transition: opacity 0.5s ease;
}

.carousel-slide.active {
  opacity: 1;
}

.carousel-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.carousel-content {
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  padding: 60px;
  background: linear-gradient(to top, rgba(0, 0, 0, 0.8), transparent);
  color: white;
}

.carousel-title {
  font-size: 36px;
  font-weight: 700;
  margin: 0 0 10px;
}

.carousel-description {
  font-size: 18px;
  margin: 0;
  max-width: 600px;
}

.carousel-btn {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background-color: rgba(255, 255, 255, 0.3);
  color: white;
  border: none;
  border-radius: 50%;
  width: 50px;
  height: 50px;
  font-size: 24px;
  cursor: pointer;
  transition: background-color 0.3s ease;
  z-index: 10;
}

.carousel-btn:hover {
  background-color: rgba(255, 255, 255, 0.5);
}

.carousel-btn.prev {
  left: 20px;
}

.carousel-btn.next {
  right: 20px;
}

.carousel-indicators {
  position: absolute;
  bottom: 20px;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  gap: 10px;
  z-index: 10;
}

.carousel-indicator {
  width: 12px;
  height: 12px;
  border-radius: 50%;
  background-color: rgba(255, 255, 255, 0.5);
  border: none;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.carousel-indicator.active {
  background-color: white;
}

/* 商品展示样式 */
.products-section {
  padding: 80px 0;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
}

.section-title {
  font-size: 32px;
  font-weight: 700;
  text-align: center;
  margin: 0 0 60px;
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
  position: relative;
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
  margin: 0 0 5px;
}

.product-model {
  font-size: 12px;
  color: #999;
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

/* 分类导航样式 */
.categories-section {
  padding: 80px 0;
  background-color: #f8f8f8;
}

.categories-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  gap: 30px;
}

.category-card {
  background-color: white;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.category-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.15);
}

.category-image {
  width: 100%;
  height: 200px;
  overflow: hidden;
}

.category-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.3s ease;
}

.category-card:hover .category-image img {
  transform: scale(1.05);
}

.category-content {
  padding: 20px;
  text-align: center;
}

.category-name {
  font-size: 18px;
  font-weight: 600;
  margin: 0 0 5px;
  color: #333;
}

.category-count {
  font-size: 14px;
  color: #666;
  margin: 0;
}

/* 品牌理念样式 */
.brand-section {
  padding: 100px 0;
}

.brand-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 60px;
  align-items: center;
}

.brand-text {
  padding: 20px 0;
}

.brand-description {
  font-size: 16px;
  line-height: 1.6;
  color: #666;
  margin: 0 0 30px;
}

.brand-link {
  display: inline-block;
  padding: 12px 24px;
  background-color: #333;
  color: white;
  border-radius: 4px;
  font-weight: 600;
  transition: background-color 0.3s ease, transform 0.3s ease;
}

.brand-link:hover {
  background-color: #555;
  transform: translateY(-2px);
  color: white;
}

.brand-image {
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

.brand-image img {
  width: 100%;
  height: auto;
  object-fit: cover;
}

/* 客户评价样式 */
.testimonials-section {
  padding: 80px 0;
  background-color: #f8f8f8;
}

.testimonials-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 40px;
}

.testimonial-card {
  background-color: white;
  padding: 30px;
  border-radius: 8px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  text-align: center;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.testimonial-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.15);
}

.testimonial-avatar {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  overflow: hidden;
  margin: 0 auto 20px;
}

.testimonial-avatar img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.testimonial-rating {
  margin: 0 0 15px;
}

.testimonial-comment {
  font-size: 14px;
  line-height: 1.6;
  color: #666;
  margin: 0 0 20px;
  font-style: italic;
}

.testimonial-name {
  font-size: 16px;
  font-weight: 600;
  color: #333;
  margin: 0;
}

/* 特色商品样式 */
.featured-section {
  padding: 80px 0;
}

.featured-badge {
  position: absolute;
  top: 10px;
  right: 10px;
  background-color: #333;
  color: white;
  padding: 5px 10px;
  border-radius: 4px;
  font-size: 12px;
  font-weight: 600;
  z-index: 10;
}

/* 促销模块样式 */
.promotion-section {
  padding: 80px 0;
  background-color: #f0f0f0;
}

.promotion-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 60px;
  align-items: center;
  background-color: white;
  border-radius: 8px;
  padding: 40px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

.promotion-text {
  padding: 20px 0;
}

.promotion-title {
  font-size: 28px;
  font-weight: 700;
  margin: 0 0 15px;
  color: #333;
}

.promotion-description {
  font-size: 16px;
  line-height: 1.6;
  color: #666;
  margin: 0 0 30px;
}

.promotion-link {
  display: inline-block;
  padding: 12px 24px;
  background-color: #333;
  color: white;
  border-radius: 4px;
  font-weight: 600;
  transition: background-color 0.3s ease, transform 0.3s ease;
}

.promotion-link:hover {
  background-color: #555;
  transform: translateY(-2px);
  color: white;
}

.promotion-image {
  border-radius: 8px;
  overflow: hidden;
}

.promotion-image img {
  width: 100%;
  height: auto;
  object-fit: cover;
}

/* 响应式设计 */
@media (max-width: 768px) {
  .carousel {
    height: 400px;
  }

  .carousel-content {
    padding: 40px;
  }

  .carousel-title {
    font-size: 28px;
  }

  .carousel-description {
    font-size: 16px;
  }

  .products-grid {
    grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
    gap: 30px;
  }

  .products-section,
  .categories-section,
  .brand-section,
  .testimonials-section,
  .featured-section,
  .promotion-section {
    padding: 60px 0;
  }

  .section-title {
    font-size: 28px;
    margin-bottom: 40px;
  }

  .brand-content,
  .promotion-content {
    grid-template-columns: 1fr;
    gap: 40px;
  }

  .categories-grid {
    grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
    gap: 20px;
  }

  .testimonials-grid {
    grid-template-columns: 1fr;
    gap: 30px;
  }

  .promotion-content {
    padding: 30px;
  }

  .promotion-title {
    font-size: 24px;
  }
}

@media (max-width: 480px) {
  .carousel {
    height: 300px;
  }

  .carousel-content {
    padding: 30px;
  }

  .carousel-title {
    font-size: 24px;
  }

  .carousel-description {
    font-size: 14px;
  }

  .section-title {
    font-size: 24px;
  }

  .brand-description,
  .promotion-description {
    font-size: 14px;
  }

  .promotion-content {
    padding: 20px;
  }
}
</style>