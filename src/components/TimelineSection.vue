<template>
  <section id="timeline" class="timeline">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title">{{ historyData.section_title }}</h2>
      </div>
      <div class="timeline-content">
        <div class="timeline-items">
          <div class="timeline-item" v-for="(item, index) in historyData.timeline" :key="index">
            <div class="timeline-dot">
              <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <circle cx="12" cy="12" r="10"/>
              </svg>
            </div>
            <div class="timeline-date">{{ item.date }}</div>
            <div class="timeline-title">{{ item.event }}</div>
          </div>
        </div>
        <div class="timeline-actions">
          <button 
            v-for="(action, index) in historyData.actions" 
            :key="index" 
            class="timeline-btn"
            @click="handleAction(action.action_url)"
          >
            {{ action.label }}
          </button>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const historyData = ref({
  section_title: '学習の軌跡',
  timeline: [],
  actions: []
});

const jsonModules = import.meta.glob('../json/*.json', { eager: true });

onMounted(() => {
  if (jsonModules['../json/learning-history.json']) {
    historyData.value = jsonModules['../json/learning-history.json'].default;
  }
});

const handleAction = (url) => {
  if (url) {
    window.location.href = url;
  }
};
</script>

<style scoped>
.timeline {
  padding: 80px 0;
  background: white;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 24px;
}

.section-header {
  margin-bottom: 48px;
}

.section-title {
  font-size: 28px;
  font-weight: 700;
  color: #1f2937;
  margin: 0;
}

.timeline-content {
  display: flex;
  align-items: center;
  gap: 48px;
}

.timeline-items {
  display: flex;
  flex: 1;
  justify-content: space-between;
  position: relative;
}

.timeline-items::before {
  content: "";
  position: absolute;
  top: 24px;
  left: 0;
  right: 0;
  height: 2px;
  background: #e5e7eb;
}

.timeline-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 8px;
  position: relative;
  z-index: 1;
}

.timeline-dot {
  width: 48px;
  height: 48px;
  background: #2563eb;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  box-shadow: 0 4px 12px rgba(37, 99, 235, 0.3);
}

.timeline-date {
  font-size: 13px;
  font-weight: 600;
  color: #374151;
}

.timeline-title {
  font-size: 13px;
  color: #6b7280;
  text-align: center;
}

.timeline-actions {
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.timeline-btn {
  padding: 10px 20px;
  background: #f3f4f6;
  color: #374151;
  border: none;
  border-radius: 8px;
  font-size: 13px;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.2s;
}

.timeline-btn:hover {
  background: #e5e7eb;
}
</style>