<template>
  <section id="about" class="about">
    <div class="container">
      <div class="about-grid">
        <div class="about-card">
          <h3 class="card-title">{{ aboutData.about.title }}</h3>
          <div class="about-content">
            <img :src="aboutData.about.profile_image" alt="プロフィール画像" class="about-image">
            <div class="about-info">
              <p class="about-text">
                {{ aboutData.about.greeting }}<br>
                {{ aboutData.about.description }}
              </p>
              <div class="about-details">
                <div class="detail-item" v-for="detail in aboutData.about.details" :key="detail.label">
                  <span class="detail-label">{{ detail.label }}</span>
                  <span class="detail-value">{{ detail.value }}</span>
                </div>
              </div>
            </div>
          </div>
        </div>

        <div id="contact" class="contact-card">
          <h3 class="card-title">{{ aboutData.contact.title }}</h3>
          <div class="contact-list">
            <div class="contact-item" v-for="(item, index) in aboutData.contact.items" :key="index">
              <component :is="getIconComponent(item.type)" />
              <span class="contact-value">{{ item.value }}</span>
              <button 
                v-if="item.type === 'email' || item.type === 'github'"
                class="copy-btn" 
                @click="copyToClipboard(item.value)"
                :class="{ copied: copiedIndex === index }"
              >
                {{ copiedIndex === index ? '完了' : 'コピー' }}
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <transition name="fade">
      <div v-if="showToast" class="copy-toast">
        <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
          <path d="M20 6L9 17l-5-5"/>
        </svg>
        <span>コピーしました</span>
      </div>
    </transition>
  </section>
</template>

<script setup>
import { ref, onMounted, h } from 'vue';

const aboutData = ref({
  about: {
    title: '自己紹介',
    profile_image: '',
    greeting: '',
    description: '',
    details: []
  },
  contact: {
    title: '連絡先',
    items: []
  }
});

const jsonModules = import.meta.glob('../json/*.json', { eager: true });

onMounted(() => {
  if (jsonModules['../json/about.json']) {
    aboutData.value = jsonModules['../json/about.json'].default;
  }
});

const getIconComponent = (type) => {
  const icons = {
    email: () => h('svg', { width: '20', height: '20', viewBox: '0 0 24 24', fill: 'none', stroke: 'currentColor', 'stroke-width': '2' }, [
      h('path', { d: 'M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z' }),
      h('polyline', { points: '22,6 12,13 2,6' })
    ]),
    github: () => h('svg', { width: '20', height: '20', viewBox: '0 0 24 24', fill: 'none', stroke: 'currentColor', 'stroke-width': '2' }, [
      h('path', { d: 'M15 21v-2a4 4 0 0 0-4-4H5a4 4 0 0 0-4 4v2' }),
      h('circle', { cx: '12', cy: '7', r: '4' })
    ]),
    location: () => h('svg', { width: '20', height: '20', viewBox: '0 0 24 24', fill: 'none', stroke: 'currentColor', 'stroke-width': '2' }, [
      h('path', { d: 'M21 10c0 7-9 13-9 13s-9-6-9-13a9 9 0 0 1 18 0z' }),
      h('circle', { cx: '12', cy: '10', r: '3' })
    ])
  };
  return icons[type] || icons.location;
};

const copiedIndex = ref(-1);
const showToast = ref(false);

const copyToClipboard = async (text) => {
  try {
    await navigator.clipboard.writeText(text);
    copiedIndex.value = aboutData.value.contact.items.findIndex(item => item.value === text);
    
    showToast.value = true;
    setTimeout(() => {
      showToast.value = false;
    }, 2000);
    
    setTimeout(() => {
      copiedIndex.value = -1;
    }, 2000);
  } catch (err) {
    console.error('Failed to copy:', err);
  }
};
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

.contact-value {
  flex: 1;
  min-width: 0;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

.contact-item svg {
  color: #6b7280;
  flex-shrink: 0;
}

.copy-btn {
  padding: 6px 12px;
  background: #f3f4f6;
  border: none;
  border-radius: 6px;
  color: #6b7280;
  cursor: pointer;
  transition: all 0.2s;
  flex-shrink: 0;
  min-width: 56px;
  height: 32px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 12px;
  font-weight: 500;
}

.copy-btn:hover {
  background: #e5e7eb;
  color: #374151;
}

.copy-btn.copied {
  background: #dcfce7;
  color: #16a34a;
}

.copy-toast {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background: #1f2937;
  color: white;
  padding: 16px 24px;
  border-radius: 8px;
  display: flex;
  align-items: center;
  gap: 12px;
  font-size: 14px;
  font-weight: 500;
  z-index: 1000;
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.3);
}

.copy-toast svg {
  color: #10b981;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease, transform 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
  transform: translate(-50%, -50%) scale(0.9);
}
</style>