<template>
  <section id="about" class="about">
    <div class="container">
      <div class="about-grid">
        <div class="about-card">
          <h3 class="card-title">自己紹介</h3>
          <div class="about-content">
            <img src="https://neeko-copilot.bytedance.net/api/text2image?prompt=professional%20asian%20male%20software%20engineer%20portrait%20photo%20formal&image_size=portrait_4_3" alt="プロフィール画像" class="about-image">
            <div class="about-info">
              <p class="about-text">
                はじめまして、練潮田（れんちょうでん）です。<br>
                中国出身で、現在は日本でエンジニアとしてキャリアを目指しています。<br>
                プログラミングが大好きで、問題解決や新しい技術の学習にやりがいを感じます。<br>
                チームで働くこと、ユーザーに価値を提供できるサービスを<br>
                開発したいと考えています。
              </p>
              <div class="about-details">
                <div class="detail-item">
                  <span class="detail-label">年齢</span>
                  <span class="detail-value">24歳</span>
                </div>
                <div class="detail-item">
                  <span class="detail-label">在住</span>
                  <span class="detail-value">日本・東京</span>
                </div>
                <div class="detail-item">
                  <span class="detail-label">日本語</span>
                  <span class="detail-value">N1</span>
                </div>
                <div class="detail-item">
                  <span class="detail-label">就業形態</span>
                  <span class="detail-value">正社員・技術・人文知識・国際業務（予定）</span>
                </div>
              </div>
            </div>
          </div>
        </div>

        <div id="contact" class="contact-card">
          <h3 class="card-title">連絡先</h3>
          <div class="contact-list">
            <div class="contact-item">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/>
                <polyline points="22,6 12,13 2,6"/>
              </svg>
              <span>example@email.com</span>
            </div>
            <div class="contact-item">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <path d="M15 21v-2a4 4 0 0 0-4-4H5a4 4 0 0 0-4 4v2"/>
                <circle cx="12" cy="7" r="4"/>
              </svg>
              <span>github.com/example</span>
            </div>
            <div class="contact-item">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <path d="M21 10c0 7-9 13-9 13s-9-6-9-13a9 9 0 0 1 18 0z"/>
                <circle cx="12" cy="10" r="3"/>
              </svg>
              <span>日本・東京</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
</script>

<style scoped>
.about {
  padding: 80px 0;
  background: #f9fafb;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 24px;
}

.about-grid {
  display: grid;
  grid-template-columns: 2fr 1fr;
  gap: 24px;
}

.about-card,
.contact-card {
  background: white;
  padding: 24px;
  border-radius: 16px;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
}

.card-title {
  font-size: 20px;
  font-weight: 700;
  color: #1f2937;
  margin: 0 0 20px;
}

.about-content {
  display: flex;
  gap: 20px;
}

.about-image {
  width: 160px;
  height: 200px;
  object-fit: cover;
  border-radius: 12px;
  flex-shrink: 0;
}

.about-info {
  flex: 1;
}

.about-text {
  font-size: 14px;
  color: #4b5563;
  line-height: 1.8;
  margin: 0 0 20px;
}

.about-details {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 12px;
}

.detail-item {
  display: flex;
  flex-direction: column;
  gap: 4px;
}

.detail-label {
  font-size: 12px;
  color: #9ca3af;
}

.detail-value {
  font-size: 14px;
  font-weight: 500;
  color: #374151;
}

.contact-list {
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.contact-item {
  display: flex;
  align-items: center;
  gap: 12px;
  color: #374151;
  font-size: 14px;
}

.contact-item svg {
  color: #6b7280;
  flex-shrink: 0;
}
</style>