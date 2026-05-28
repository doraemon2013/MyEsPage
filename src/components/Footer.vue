<template>
  <footer class="footer">
    <div class="container">
      <div class="footer-content">
        <div class="footer-brand">
          <div class="logo">
            <svg width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <path d="M12 2L2 7l10 5 10-5-10-5zM2 17l10 5 10-5M2 12l10 5 10-5"/>
            </svg>
            <span class="brand-name">練潮田</span>
          </div>
          <p class="footer-text">Webエンジニアとして、日々学習と成長を続けています。</p>
        </div>
        <div class="footer-links">
          <h4 class="footer-title">リンク</h4>
          <ul>
            <li><a href="#">ホーム</a></li>
            <li><a href="#skills">スキル</a></li>
            <li><a href="#projects">プロジェクト</a></li>
            <li><a href="#timeline">学習記録</a></li>
          </ul>
        </div>
        <div class="footer-links">
          <h4 class="footer-title">サービス</h4>
          <ul>
            <li><a href="#">Web開発</a></li>
            <li><a href="#">API開発</a></li>
            <li><a href="#">システム設計</a></li>
            <li><a href="#">技術コンサル</a></li>
          </ul>
        </div>
        <div class="footer-links">
          <h4 class="footer-title">連絡先</h4>
          <ul>
            <li>example@email.com</li>
            <li>github.com/example</li>
            <li>日本・東京</li>
          </ul>
        </div>
      </div>
      <div class="footer-bottom">
        <p>&copy; 2025 練潮田. All rights reserved.</p>
      </div>
    </div>
  </footer>
</template>

<script setup>
</script>

<style scoped>
.footer {
  background: #1f2937;
  color: white;
  padding: 48px 0 24px;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 24px;
}

.footer-content {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 32px;
  margin-bottom: 32px;
}

.footer-brand {
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.logo {
  display: flex;
  align-items: center;
  gap: 10px;
  color: #2563eb;
}

.brand-name {
  font-weight: 700;
  font-size: 16px;
  color: white;
}

.footer-text {
  font-size: 14px;
  color: #9ca3af;
  line-height: 1.6;
}

.footer-links {
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.footer-title {
  font-size: 14px;
  font-weight: 600;
  color: #f3f4f6;
  margin: 0;
}

.footer-links ul {
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.footer-links a {
  text-decoration: none;
  color: #9ca3af;
  font-size: 13px;
  transition: color 0.2s;
}

.footer-links a:hover {
  color: white;
}

.footer-links li:last-child {
  color: #9ca3af;
  font-size: 13px;
}

.footer-bottom {
  border-top: 1px solid #374151;
  padding-top: 24px;
}

.footer-bottom p {
  text-align: center;
  font-size: 13px;
  color: #6b7280;
  margin: 0;
}
</style>