<template>
  <footer class="footer">
    <div class="footer-container">
      <div class="footer-info">
        <h3 class="footer-title">极简家居</h3>
        <p class="footer-description">专注于提供简约、高品质的家居用品</p>
      </div>
      <div class="footer-links">
        <h4 class="footer-subtitle">快速链接</h4>
        <ul class="footer-menu">
          <li><router-link to="/" class="footer-link">首页</router-link></li>
          <li><router-link to="/search" class="footer-link">搜索</router-link></li>
          <li><router-link to="/about" class="footer-link">关于我们</router-link></li>
        </ul>
      </div>
      <div class="footer-contact">
        <h4 class="footer-subtitle">联系我们</h4>
        <p class="footer-contact-item">邮箱: contact@minimalhome.com</p>
        <p class="footer-contact-item">电话: 400-123-4567</p>
      </div>
    </div>
    <div class="footer-bottom">
      <p class="footer-copyright">© 2026 极简家居. 保留所有权利.</p>
    </div>
  </footer>
</template>

<style scoped>
.footer {
  background-color: #f8f8f8;
  padding: 40px 0 20px;
  margin-top: 40px;
}

.footer-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 40px;
}

.footer-title {
  font-size: 20px;
  font-weight: 700;
  margin: 0 0 10px;
  color: #333;
}

.footer-description {
  font-size: 14px;
  color: #666;
  margin: 0;
}

.footer-subtitle {
  font-size: 16px;
  font-weight: 600;
  margin: 0 0 15px;
  color: #333;
}

.footer-menu {
  list-style: none;
  margin: 0;
  padding: 0;
}

.footer-link {
  color: #666;
  text-decoration: none;
  font-size: 14px;
  line-height: 1.6;
  transition: color 0.3s ease;
}

.footer-link:hover {
  color: #333;
}

.footer-contact-item {
  font-size: 14px;
  color: #666;
  margin: 0 0 8px;
}

.footer-bottom {
  margin-top: 40px;
  padding-top: 20px;
  border-top: 1px solid #eee;
  text-align: center;
}

.footer-copyright {
  font-size: 14px;
  color: #999;
  margin: 0;
}

@media (max-width: 768px) {
  .footer-container {
    grid-template-columns: 1fr;
    gap: 30px;
    text-align: center;
  }
}
</style>