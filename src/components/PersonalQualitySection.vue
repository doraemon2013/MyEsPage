<template>
  <section class="personal-quality">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title">{{ qualityData.section_title }}</h2>
      </div>
      <div class="quality-card">
        <div class="quality-left">
          <div class="image-carousel" v-if="currentAbility.images.length > 0">
            <div class="carousel-wrapper">
              <div class="carousel-track" :style="{ transform: `translateX(-${currentImageIndex * 100}%)` }">
                <div 
                  v-for="(image, index) in currentAbility.images" 
                  :key="index"
                  class="carousel-slide"
                >
                  <img :src="image" :alt="currentAbility.label" class="carousel-image" />
                </div>
              </div>
            </div>
            <div class="carousel-controls" v-if="currentAbility.images.length > 1">
              <button class="carousel-prev" @click="prevImage">
                <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <path d="M15 19l-7-7 7-7"/>
                </svg>
              </button>
              <div class="carousel-dots">
                <span 
                  v-for="(image, index) in currentAbility.images" 
                  :key="index"
                  class="dot"
                  :class="{ active: currentImageIndex === index }"
                  @click="currentImageIndex = index"
                ></span>
              </div>
              <button class="carousel-next" @click="nextImage">
                <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <path d="M9 5l7 7-7 7"/>
                </svg>
              </button>
            </div>
          </div>
        </div>
        <div class="quality-center">
          <h3 class="ability-title">{{ currentAbility.label }}</h3>
          <p class="ability-description">{{ currentAbility.description }}</p>
          <div class="ability-value">
            <span class="value-label">スコア</span>
            <span class="value-number">{{ currentAbility.value }}</span>
          </div>
        </div>
        <div class="quality-right">
          <div class="strengths-list">
            <h4 class="strengths-title">強み</h4>
            <div class="strength-item" 
                 v-for="(ability, index) in qualityData.abilities" 
                 :key="ability.id"
                 :class="{ active: currentIndex === index }"
                 @click="selectAbility(index)"
            >
              <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <path d="M20 6L9 17l-5-5"/>
              </svg>
              <span>{{ ability.label }}</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue';

const qualityData = ref({
  section_title: '個人の強み',
  description: '',
  abilities: []
});

const currentIndex = ref(0);
const currentImageIndex = ref(0);

const jsonModules = import.meta.glob('../json/*.json', { eager: true });

onMounted(() => {
  if (jsonModules['../json/key-trengths.json']) {
    qualityData.value = { ...qualityData.value, ...jsonModules['../json/key-trengths.json'].default };
  }
});

const currentAbility = computed(() => {
  return qualityData.value.abilities[currentIndex.value] || { label: '', description: '', value: 0, images: [] };
});

const selectAbility = (index) => {
  currentIndex.value = index;
  currentImageIndex.value = 0;
};

const nextImage = () => {
  if (currentAbility.value && currentAbility.value.images.length > 1) {
    currentImageIndex.value = (currentImageIndex.value + 1) % currentAbility.value.images.length;
  }
};

const prevImage = () => {
  if (currentAbility.value && currentAbility.value.images.length > 1) {
    currentImageIndex.value = (currentImageIndex.value - 1 + currentAbility.value.images.length) % currentAbility.value.images.length;
  }
};
</script>

<style scoped>
.personal-quality {
  padding: 60px 0;
  background: linear-gradient(135deg, #f8fafc 0%, #f1f5f9 100%);
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 24px;
}

.section-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 40px;
}

.section-title {
  font-size: 32px;
  font-weight: 700;
  color: #1f2937;
  margin: 0;
}

.quality-card {
  display: grid;
  grid-template-columns: 1.2fr 1fr 0.8fr;
  gap: 32px;
  background: white;
  border-radius: 16px;
  padding: 40px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.08);
  min-height: 450px;
}

.quality-left {
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.image-carousel {
  width: 100%;
}

.carousel-wrapper {
  overflow: hidden;
  border-radius: 12px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

.carousel-track {
  display: flex;
  transition: transform 0.4s ease;
}

.carousel-slide {
  flex: 0 0 100%;
}

.carousel-image {
  width: 100%;
  height: 340px;
  object-fit: cover;
}

.carousel-controls {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 16px;
  margin-top: 16px;
}

.carousel-prev,
.carousel-next {
  padding: 8px;
  background: #f1f5f9;
  border: none;
  border-radius: 50%;
  color: #64748b;
  cursor: pointer;
  transition: all 0.2s;
}

.carousel-prev:hover,
.carousel-next:hover {
  background: #e2e8f0;
  color: #374151;
}

.carousel-dots {
  display: flex;
  gap: 8px;
}

.dot {
  width: 8px;
  height: 8px;
  background: #cbd5e1;
  border-radius: 50%;
  cursor: pointer;
  transition: all 0.2s;
}

.dot.active {
  background: #3b82f6;
}

.quality-center {
  display: flex;
  flex-direction: column;
  justify-content: center;
  gap: 20px;
  padding: 20px 0;
}

.ability-title {
  font-size: 28px;
  font-weight: 700;
  color: #1e293b;
  margin: 0;
  line-height: 1.3;
}

.ability-description {
  font-size: 15px;
  color: #64748b;
  line-height: 1.8;
  margin: 0;
}

.ability-value {
  display: flex;
  flex-direction: column;
  gap: 8px;
  padding-top: 16px;
  border-top: 2px solid #f1f5f9;
}

.value-label {
  font-size: 14px;
  color: #94a3b8;
  font-weight: 500;
}

.value-number {
  font-size: 48px;
  font-weight: 700;
  color: #3b82f6;
}

.quality-right {
  display: flex;
  align-items: flex-start;
  justify-content: flex-end;
}

.strengths-list {
  width: 100%;
  max-width: 240px;
}

.strengths-title {
  font-size: 18px;
  font-weight: 700;
  color: #1f2937;
  margin: 0 0 20px 0;
}

.strength-item {
  display: flex;
  align-items: flex-start;
  gap: 10px;
  padding: 10px 14px;
  border-radius: 8px;
  margin-bottom: 6px;
  cursor: pointer;
  transition: all 0.2s;
  color: #374151;
  font-size: 13px;
  line-height: 1.5;
}

.strength-item svg {
  color: #22c55e;
  flex-shrink: 0;
  margin-top: 2px;
  flex-shrink: 0;
}

.strength-item span {
  flex: 1;
  word-break: break-word;
}

.strength-item:hover {
  background: #f8fafc;
}

.strength-item.active {
  background: #eff6ff;
  color: #2563eb;
  font-weight: 500;
}

.strength-item.active svg {
  color: #2563eb;
}

@media (max-width: 1024px) {
  .quality-card {
    grid-template-columns: 1fr;
    gap: 24px;
    min-height: auto;
  }
  
  .quality-center {
    order: 2;
  }
  
  .quality-right {
    order: 3;
    align-items: flex-start;
  }
  
  .carousel-image {
    height: 220px;
  }
}

@media (max-width: 768px) {
  .section-title {
    font-size: 24px;
  }
  
  .quality-card {
    padding: 24px;
  }
  
  .ability-title {
    font-size: 22px;
  }
  
  .ability-description {
    font-size: 14px;
  }
  
  .value-number {
    font-size: 36px;
  }
  
  .carousel-image {
    height: 180px;
  }
  
  .strength-item {
    font-size: 13px;
    padding: 10px 14px;
  }
}
</style>