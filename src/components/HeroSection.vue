<template>
  <section class="hero">
    <div class="container">
      <div class="hero-content">
        <div class="hero-left">
          <transition name="fade" mode="out-in">
            <div :key="currentPage">
              <div class="tags">
                <span class="tag" v-for="tag in pages[currentPage].tags" :key="tag">{{ tag }}</span>
              </div>
              <h1 class="hero-title">{{ pages[currentPage].title }}</h1>
              <h2 class="hero-subtitle">{{ pages[currentPage].subtitle }}</h2>
              <p class="hero-description">{{ pages[currentPage].description }}</p>
              <div class="stats">
                <div class="stat-item" v-for="stat in pages[currentPage].stats" :key="stat.label">
                  <div class="stat-value">{{ stat.value }}</div>
                  <div class="stat-label">{{ stat.label }}</div>
                </div>
              </div>
              <div class="hero-actions">
                <button class="btn-primary">{{ pages[currentPage].primaryBtn }}</button>
                <button class="btn-secondary">{{ pages[currentPage].secondaryBtn }}</button>
              </div>
            </div>
          </transition>
        </div>
        <div class="hero-right">
          <div class="hero-image-wrapper">
            <transition name="fade" mode="out-in">
              <img :key="currentPage" :src="pages[currentPage].image" :alt="pages[currentPage].title" class="hero-image">
            </transition>
          </div>
          <div class="strength-card" @mouseenter="handleCardMouseEnter" @mouseleave="handleCardMouseLeave">
            <h3 class="strength-title">強み</h3>
            <ul class="strength-list">
              <li 
                v-for="(item, index) in strengths" 
                :key="index"
                @mouseenter="(e) => { e.stopPropagation(); handleItemMouseEnter(index); }"
                :class="{ active: currentPage === index }"
              >
                <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="3">
                  <polyline points="20 6 9 17 4 12"/>
                </svg>
                <span>{{ item }}</span>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

const currentPage = ref(0);
let autoplayTimer = null;
let delayTimer = null;
const isHovering = ref(false);
const hasInteracted = ref(false);

const nextPage = () => {
  currentPage.value = (currentPage.value + 1) % pages.length;
};

const startAutoplay = () => {
  if (autoplayTimer) return;
  autoplayTimer = setInterval(() => {
    if (!isHovering.value) {
      nextPage();
    }
  }, 5000);
};

const stopAutoplay = () => {
  if (autoplayTimer) {
    clearInterval(autoplayTimer);
    autoplayTimer = null;
  }
};

const clearDelayTimer = () => {
  if (delayTimer) {
    clearTimeout(delayTimer);
    delayTimer = null;
  }
};

const handleCardMouseEnter = () => {
  isHovering.value = true;
  clearDelayTimer();
};

const handleCardMouseLeave = () => {
  isHovering.value = false;
  if (hasInteracted.value) {
    delayTimer = setTimeout(() => {
      if (!isHovering.value && !autoplayTimer) {
        startAutoplay();
      }
    }, 15000);
  }
};

const handleItemMouseEnter = (index) => {
  hasInteracted.value = true;
  stopAutoplay();
  currentPage.value = index;
};

onMounted(() => {
  startAutoplay();
});

onUnmounted(() => {
  stopAutoplay();
  clearDelayTimer();
});

const strengths = [
  '日語対応能力（N1）',
  '学習意欲が高く、継続できる',
  '自走力があり、課題解決が得意',
  'チームで協力して成果を出す',
  '日本で長期的に働きたい'
];

const pages = [
  {
    title: '学び続け、価値を創造する',
    subtitle: 'Webエンジニア',
    description: '日本で長期的にキャリアを築くことを目指し、日々学習と実践を積み重ねています。技術の人の役に立つサービスを開発し、チームと共に成長していきたいです。',
    tags: ['Java', 'Spring Boot', 'Vue.js'],
    stats: [
      { value: 'N1', label: '日本語能力' },
      { value: '情報処理技術者', label: '資格' },
      { value: '複数プロジェクト', label: '開発経験' },
      { value: '日本での就職', label: '目標' }
    ],
    primaryBtn: 'プロジェクトを見る',
    secondaryBtn: 'GitHub',
    image: 'https://neeko-copilot.bytedance.net/api/text2image?prompt=professional%20asian%20male%20software%20engineer%20looking%20at%20sunset%20view%20from%20mountain%20top%20silhouette%20style&image_size=portrait_4_3'
  },
  {
    title: '日本語能力 N1',
    subtitle: '言語スキル',
    description: '日本語能力試験N1レベルを取得しており、日常会話から業務上の技術的な議論までスムーズに対応することができます。',
    tags: ['日本語', 'N1', 'コミュニケーション'],
    stats: [
      { value: 'N1', label: '日本語能力' },
      { value: 'TOEIC 900+', label: '英語能力' },
      { value: '母国語', label: '中国語' },
      { value: '3ヶ国語', label: '対応可能' }
    ],
    primaryBtn: '履歴書を見る',
    secondaryBtn: '詳細',
    image: 'https://neeko-copilot.bytedance.net/api/text2image?prompt=professional%20language%20learning%20study%20japanese%20kanji%20education%20modern%20clean&image_size=portrait_4_3'
  },
  {
    title: '学習意欲が高い',
    subtitle: '成長マインドセット',
    description: '新しい技術を積極的に学び、自分自身を成長させることに情熱を注いでいます。継続的な学習を通じてスキルアップを目指しています。',
    tags: ['学習', '成長', 'スキルアップ'],
    stats: [
      { value: '500+', label: '学習時間' },
      { value: '20+', label: '技術書' },
      { value: '10+', label: 'オンラインコース' },
      { value: '毎日', label: '学習習慣' }
    ],
    primaryBtn: '学習記録',
    secondaryBtn: '資格',
    image: 'https://neeko-copilot.bytedance.net/api/text2image?prompt=modern%20study%20desk%20with%20books%20laptop%20programming%20learning%20environment&image_size=portrait_4_3'
  },
  {
    title: '課題解決が得意',
    subtitle: '問題解決能力',
    description: '複雑な問題に直面したとき、論理的に分析し、最適な解決策を見つけ出すことができます。自走力があり、独立して作業を進めることができます。',
    tags: ['問題解決', '論理思考', '自走力'],
    stats: [
      { value: '100+', label: 'バグ修正' },
      { value: '50+', label: '技術課題' },
      { value: '95%', label: '解決率' },
      { value: '自主的', label: '問題発見' }
    ],
    primaryBtn: 'プロジェクト',
    secondaryBtn: '実績',
    image: 'https://neeko-copilot.bytedance.net/api/text2image?prompt=problem%20solving%20brainstorming%20whiteboard%20code%20debugging%20modern%20office&image_size=portrait_4_3'
  },
  {
    title: 'チームで協力',
    subtitle: 'チームプレイヤー',
    description: 'チームメンバーと協力し、目標達成のために貢献することを重視しています。コミュニケーションを大切にし、良いチーム環境を作り出すことができます。',
    tags: ['チームワーク', 'コミュニケーション', '協力'],
    stats: [
      { value: '10+', label: 'チームプロジェクト' },
      { value: 'Scrum', label: '開発手法' },
      { value: '積極的', label: '意見発言' },
      { value: 'リーダー', label: '経験有' }
    ],
    primaryBtn: 'チーム経験',
    secondaryBtn: '紹介',
    image: 'https://neeko-copilot.bytedance.net/api/text2image?prompt=team%20collaboration%20meeting%20modern%20office%20developers%20working%20together&image_size=portrait_4_3'
  },
  {
    title: '日本で働きたい',
    subtitle: 'キャリア目標',
    description: '日本のテクノロジー企業で長期的に働き、日本のIT業界に貢献したいと考えています。文化やビジネス習慣を理解し、地元のチームに溶け込むことを目指しています。',
    tags: ['就職活動', '長期勤務', '日本'],
    stats: [
      { value: '2024', label: '就職目標' },
      { value: '東京', label: '希望勤務地' },
      { value: '正社員', label: '雇用形態' },
      { value: '永住', label: '長期目標' }
    ],
    primaryBtn: 'ESを見る',
    secondaryBtn: '連絡',
    image: 'https://neeko-copilot.bytedance.net/api/text2image?prompt=tokyo%20city%20skyline%20modern%20office%20building%20japanese%20technology%20company&image_size=portrait_4_3'
  }
];
</script>

<style scoped>
.hero {
  padding: 120px 0 80px;
  background: linear-gradient(135deg, #f8fafc 0%, #e0f2fe 100%);
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 24px;
}

.hero-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 64px;
  align-items: start;
  min-height: 580px;
}

.hero-left {
  display: flex;
  flex-direction: column;
  justify-content: center;
  min-height: 500px;
}

.fade-enter-active,
.fade-leave-active {
  transition: all 0.4s ease;
}

.fade-enter-from {
  opacity: 0;
  transform: translateX(-20px);
}

.fade-leave-to {
  opacity: 0;
  transform: translateX(20px);
}

.tags {
  display: flex;
  gap: 8px;
  margin-bottom: 24px;
}

.tag {
  padding: 6px 16px;
  background: rgba(37, 99, 235, 0.1);
  color: #2563eb;
  border-radius: 20px;
  font-size: 12px;
  font-weight: 500;
}

.hero-title {
  font-size: 48px;
  font-weight: 800;
  color: #1f2937;
  margin: 0 0 16px;
  line-height: 1.2;
}

.hero-subtitle {
  font-size: 24px;
  font-weight: 600;
  color: #2563eb;
  margin: 0 0 24px;
}

.hero-description {
  font-size: 16px;
  color: #6b7280;
  line-height: 1.8;
  margin: 0 0 32px;
}

.stats {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 24px;
  margin-bottom: 32px;
}

.stat-item {
  text-align: center;
  padding: 16px;
  background: white;
  border-radius: 12px;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
  transition: all 0.3s ease;
}

.stat-value {
  font-size: 20px;
  font-weight: 700;
  color: #1f2937;
  margin-bottom: 4px;
}

.stat-label {
  font-size: 12px;
  color: #6b7280;
}

.hero-actions {
  display: flex;
  gap: 16px;
}

.btn-primary {
  padding: 12px 28px;
  background: #2563eb;
  color: white;
  border: none;
  border-radius: 8px;
  font-size: 14px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.2s;
}

.btn-primary:hover {
  background: #1d4ed8;
  transform: translateY(-2px);
}

.btn-secondary {
  padding: 12px 28px;
  background: white;
  color: #374151;
  border: 1px solid #d1d5db;
  border-radius: 8px;
  font-size: 14px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.2s;
}

.btn-secondary:hover {
  background: #f9fafb;
  border-color: #9ca3af;
}

.hero-right {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  gap: 24px;
}

.hero-image-wrapper {
  position: relative;
}

.hero-image {
  width: 320px;
  height: 400px;
  object-fit: cover;
  border-radius: 16px;
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.15);
}

.strength-card {
  background: white;
  padding: 24px;
  border-radius: 12px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05);
  width: 280px;
}

.strength-title {
  font-size: 18px;
  font-weight: 700;
  color: #1f2937;
  margin: 0 0 16px;
}

.strength-list {
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.strength-list li {
  display: flex;
  align-items: center;
  gap: 8px;
  color: #374151;
  font-size: 13px;
  padding: 8px 12px;
  border-radius: 8px;
  cursor: pointer;
  transition: all 0.2s ease;
}

.strength-list li:hover,
.strength-list li.active {
  background: rgba(37, 99, 235, 0.08);
  color: #2563eb;
}

.strength-list li:hover svg,
.strength-list li.active svg {
  color: #2563eb;
}

.strength-list svg {
  color: #22c55e;
  flex-shrink: 0;
  transition: color 0.2s ease;
}
</style>