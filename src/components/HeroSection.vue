<template>
  <section 
    class="hero"
    :style="{ backgroundImage: `url(${heroData.image_url || ''})` }"
  >
    <div class="hero-overlay"></div>
    <div class="container">
      <div class="hero-content" v-if="heroData.sections.length > 0">
        <div class="hero-left">
          <transition name="fade" mode="out-in">
            <div :key="currentPage">
              <div class="tags">
                <span class="tag" v-for="tag in heroData.sections[currentPage].tags" :key="tag">{{ tag }}</span>
              </div>
              <h1 class="hero-title">{{ heroData.sections[currentPage].title }}</h1>
              <h2 class="hero-subtitle">{{ heroData.sections[currentPage].subtitle }}</h2>
              <p class="hero-description">{{ heroData.sections[currentPage].description }}</p>
              <div class="stats">
                <div class="stat-item" v-for="stat in heroData.sections[currentPage].stats" :key="stat.label">
                  <div class="stat-value">{{ stat.value }}</div>
                  <div class="stat-label">{{ stat.label }}</div>
                </div>
              </div>
              <div class="hero-actions">
                <a 
                  v-for="btn in heroData.sections[currentPage].buttons" 
                  :key="btn.text"
                  :href="btn.href"
                  :class="btn.primary ? 'btn-primary' : 'btn-secondary'"
                  target="_blank"
                  rel="noopener noreferrer"
                >
                  {{ btn.text }}
                </a>
              </div>
            </div>
          </transition>
        </div>
        <div class="hero-right">
          <div class="strength-card" @mouseenter="handleCardMouseEnter" @mouseleave="handleCardMouseLeave">
            <h3 class="strength-title">強み</h3>
            <ul class="strength-list">
              <li 
                v-for="(item, index) in heroData.sections[currentPage].strengths" 
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
      <div v-else class="loading">
        <div class="spinner"></div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

const heroData = ref({
  sections: []
});

const currentPage = ref(0);
let autoplayTimer = null;
let delayTimer = null;
const isHovering = ref(false);
const hasInteracted = ref(false);

const jsonModules = import.meta.glob('../json/*.json', { eager: true });

onMounted(() => {
  if (jsonModules['../json/hero.json']) {
    heroData.value = jsonModules['../json/hero.json'].default;
  }
  startAutoplay();
});

onUnmounted(() => {
  stopAutoplay();
  clearDelayTimer();
});

const nextPage = () => {
  if (heroData.value.sections.length > 0) {
    currentPage.value = (currentPage.value + 1) % heroData.value.sections.length;
  }
};

const startAutoplay = () => {
  if (autoplayTimer) return;
  autoplayTimer = setInterval(() => {
    if (!isHovering.value && heroData.value.sections.length > 0) {
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
  if (index >= 0 && index < heroData.value.sections.length) {
    currentPage.value = index;
  }
};
</script>

<style scoped>
.hero {
  padding: 120px 0 80px;
  background-size: contain;
  background-position: right center;
  background-repeat: no-repeat;
  position: relative;
  min-height: 700px;
  background-color: #f8fafc;
}

.hero-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(135deg, rgba(248, 250, 252, 0.95) 0%, rgba(224, 242, 254, 0.9) 100%);
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 24px;
  position: relative;
  z-index: 1;
}

.hero-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 60px;
  align-items: center;
  min-height: 580px;
}

.hero-left {
  display: flex;
  flex-direction: column;
  gap: 24px;
}

.tags {
  display: flex;
  gap: 12px;
}

.tag {
  padding: 6px 16px;
  background: rgba(59, 130, 246, 0.1);
  color: #3b82f6;
  border-radius: 20px;
  font-size: 13px;
  font-weight: 500;
}

.hero-title {
  font-size: 48px;
  font-weight: 700;
  color: #1e293b;
  margin: 0;
  line-height: 1.2;
}

.hero-subtitle {
  font-size: 24px;
  font-weight: 600;
  color: #3b82f6;
  margin: 0;
}

.hero-description {
  font-size: 16px;
  color: #64748b;
  line-height: 1.8;
  margin: 0;
  max-width: 500px;
}

.stats {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 16px;
  margin-top: 8px;
}

.stat-item {
  background: white;
  padding: 20px;
  border-radius: 12px;
  text-align: center;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.06);
}

.stat-value {
  font-size: 24px;
  font-weight: 700;
  color: #1e293b;
}

.stat-label {
  font-size: 12px;
  color: #94a3b8;
  margin-top: 4px;
}

.hero-actions {
  display: flex;
  gap: 16px;
  margin-top: 8px;
}

.btn-primary {
  padding: 14px 32px;
  background: #3b82f6;
  color: white;
  border: none;
  border-radius: 8px;
  font-size: 15px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.2s;
}

.btn-primary:hover {
  background: #2563eb;
  transform: translateY(-2px);
}

.btn-secondary {
  padding: 14px 32px;
  background: white;
  color: #374151;
  border: 1px solid #e5e7eb;
  border-radius: 8px;
  font-size: 15px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.2s;
}

.btn-secondary:hover {
  background: #f9fafb;
  border-color: #d1d5db;
}

.hero-right {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  gap: 24px;
}

.strength-card {
  background: white;
  padding: 24px;
  border-radius: 12px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.08);
  max-width: 320px;
}

.strength-title {
  font-size: 18px;
  font-weight: 700;
  color: #1f2937;
  margin: 0 0 16px 0;
}

.strength-list {
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.strength-list li {
  display: flex;
  align-items: flex-start;
  gap: 10px;
  padding: 10px 12px;
  border-radius: 8px;
  cursor: pointer;
  transition: all 0.2s;
  font-size: 13px;
  color: #374151;
}

.strength-list li svg {
  color: #22c55e;
  flex-shrink: 0;
  margin-top: 1px;
}

.strength-list li:hover {
  background: #f8fafc;
}

.strength-list li.active {
  background: #eff6ff;
  color: #2563eb;
  font-weight: 500;
}

.strength-list li.active svg {
  color: #2563eb;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.4s ease, transform 0.4s ease;
}

.fade-enter-from {
  opacity: 0;
  transform: translateX(-20px);
}

.fade-leave-to {
  opacity: 0;
  transform: translateX(20px);
}

@media (max-width: 1024px) {
  .hero-content {
    grid-template-columns: 1fr;
    gap: 40px;
  }
  
  .hero-right {
    align-items: center;
  }
  
  .hero-image {
    max-width: 100%;
  }
}

@media (max-width: 768px) {
  .hero {
    padding: 100px 0 60px;
  }
  
  .hero-title {
    font-size: 32px;
  }
  
  .hero-subtitle {
    font-size: 18px;
  }
  
  .hero-description {
    font-size: 14px;
  }
  
  .stats {
    grid-template-columns: repeat(2, 1fr);
  }
  
  .hero-actions {
    flex-direction: column;
  }
  
  .btn-primary,
  .btn-secondary {
    width: 100%;
  }
}

.loading {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 400px;
}

.spinner {
  width: 40px;
  height: 40px;
  border: 4px solid #f3f3f3;
  border-top: 4px solid #3b82f6;
  border-radius: 50%;
  animation: spin 1s linear infinite;
}

@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}
</style>
