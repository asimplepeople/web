<template>
  <div class="about-page">
    <!-- 关于我们头部 -->
    <div class="about-header">
      <div class="container">
        <h1 class="about-title">关于我们</h1>
        <p class="about-subtitle">探索极简家居的品牌理念与故事</p>
      </div>
    </div>

    <!-- 品牌故事 -->
    <div class="brand-story">
      <div class="container">
        <div class="story-content">
          <div class="story-text">
            <h2 class="section-title">品牌故事</h2>
            <p class="story-paragraph">
              极简家居成立于2020年，致力于为现代家庭提供简约、高品质的家居用品。我们相信，好的设计应该是实用与美观的完美结合，通过去除多余的装饰，保留最本质的功能与美感，为用户创造舒适、宁静的居住环境。
            </p>
            <p class="story-paragraph">
              我们的设计理念源于北欧极简主义，注重自然材质、简洁线条和功能性，每一件产品都经过精心设计和严格品质控制，确保为用户带来最好的使用体验。
            </p>
          </div>
          <div class="story-image">
            <img src="https://trae-api-cn.mchost.guru/api/ide/v1/text_to_image?prompt=minimalist%20home%20office%20with%20clean%20design%2C%20natural%20light%2C%20simple%20furniture&image_size=landscape_16_9" alt="品牌故事" />
          </div>
        </div>
      </div>
    </div>

    <!-- 品牌理念 -->
    <div class="brand-values">
      <div class="container">
        <h2 class="section-title">品牌理念</h2>
        <div class="values-grid">
          <div class="value-item">
            <div class="value-icon">✦</div>
            <h3 class="value-title">简约设计</h3>
            <p class="value-description">去除多余装饰，保留最本质的功能与美感</p>
          </div>
          <div class="value-item">
            <div class="value-icon">✦</div>
            <h3 class="value-title">品质至上</h3>
            <p class="value-description">严格的品质控制，确保每一件产品都达到最高标准</p>
          </div>
          <div class="value-item">
            <div class="value-icon">✦</div>
            <h3 class="value-title">可持续发展</h3>
            <p class="value-description">采用环保材料，减少对环境的影响</p>
          </div>
          <div class="value-item">
            <div class="value-icon">✦</div>
            <h3 class="value-title">用户体验</h3>
            <p class="value-description">以用户需求为中心，创造舒适、实用的产品</p>
          </div>
        </div>
      </div>
    </div>

    <!-- 联系我们 -->
    <div class="contact-section">
      <div class="container">
        <h2 class="section-title">联系我们</h2>
        <div class="contact-info">
          <div class="contact-item">
            <h3 class="contact-title">邮箱</h3>
            <p class="contact-content">contact@minimalhome.com</p>
          </div>
          <div class="contact-item">
            <h3 class="contact-title">电话</h3>
            <p class="contact-content">400-123-4567</p>
          </div>
          <div class="contact-item">
            <h3 class="contact-title">地址</h3>
            <p class="contact-content">北京市朝阳区建国路88号</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.about-page {
  width: 100%;
}

/* 头部样式 */
.about-header {
  background-color: #f8f8f8;
  padding: 100px 0;
  text-align: center;
}

.about-title {
  font-size: 48px;
  font-weight: 700;
  margin: 0 0 20px;
  color: #333;
}

.about-subtitle {
  font-size: 20px;
  color: #666;
  margin: 0;
}

/* 品牌故事样式 */
.brand-story {
  padding: 100px 0;
}

.story-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 60px;
  align-items: center;
}

.story-text {
  padding: 20px 0;
}

.section-title {
  font-size: 32px;
  font-weight: 700;
  margin: 0 0 30px;
  color: #333;
}

.story-paragraph {
  font-size: 16px;
  line-height: 1.8;
  color: #666;
  margin: 0 0 20px;
}

.story-image {
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

.story-image img {
  width: 100%;
  height: auto;
  object-fit: cover;
}

/* 品牌理念样式 */
.brand-values {
  background-color: #f8f8f8;
  padding: 100px 0;
}

.values-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 40px;
}

.value-item {
  text-align: center;
  padding: 30px;
  background-color: white;
  border-radius: 8px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.value-item:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.15);
}

.value-icon {
  font-size: 32px;
  color: #333;
  margin: 0 0 20px;
}

.value-title {
  font-size: 18px;
  font-weight: 600;
  margin: 0 0 15px;
  color: #333;
}

.value-description {
  font-size: 14px;
  line-height: 1.6;
  color: #666;
  margin: 0;
}

/* 联系我们样式 */
.contact-section {
  padding: 100px 0;
}

.contact-info {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 40px;
  text-align: center;
}

.contact-item {
  padding: 30px;
  background-color: white;
  border-radius: 8px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

.contact-title {
  font-size: 18px;
  font-weight: 600;
  margin: 0 0 15px;
  color: #333;
}

.contact-content {
  font-size: 16px;
  color: #666;
  margin: 0;
}

@media (max-width: 768px) {
  .about-title {
    font-size: 36px;
  }

  .about-subtitle {
    font-size: 18px;
  }

  .story-content {
    grid-template-columns: 1fr;
    gap: 40px;
  }

  .values-grid {
    grid-template-columns: repeat(2, 1fr);
    gap: 30px;
  }

  .contact-info {
    grid-template-columns: 1fr;
    gap: 30px;
  }

  .brand-story,
  .brand-values,
  .contact-section {
    padding: 60px 0;
  }
}

@media (max-width: 480px) {
  .values-grid {
    grid-template-columns: 1fr;
  }

  .about-header {
    padding: 80px 0;
  }

  .about-title {
    font-size: 28px;
  }

  .section-title {
    font-size: 24px;
  }
}
</style>