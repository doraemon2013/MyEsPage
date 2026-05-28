<template>
  <section id="skills" class="skills">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title">{{ skillData.section_title }}</h2>
        <a :href="skillData.more_link" class="section-link" target="_blank" rel="noopener noreferrer">もっと見る →</a>
      </div>
      <div class="skills-grid">
        <div class="skill-item" v-for="skill in skillData.skills" :key="skill.name">
          <div class="skill-icon">
            <img :src="encodeURI(skill.icon_url)" :alt="skill.name" :title="skill.name" />
          </div>
          <div class="skill-name">{{ skill.name }}</div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const skillData = ref({
  section_title: 'スキル',
  more_link: '/skills',
  skills: []
});

const jsonModules = import.meta.glob('../json/*.json', { eager: true });

onMounted(() => {
  if (jsonModules['../json/skills.json']) {
    skillData.value = jsonModules['../json/skills.json'].default;
  }
});
</script>

<style scoped>
.skills {
  padding: 80px 0;
  background: white;
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
  margin-bottom: 48px;
}

.section-title {
  font-size: 28px;
  font-weight: 700;
  color: #1f2937;
  margin: 0;
}

.section-link {
  text-decoration: none;
  color: #2563eb;
  font-size: 14px;
  font-weight: 500;
}

.section-link:hover {
  text-decoration: underline;
}

.skills-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(140px, 1fr));
  gap: 24px;
}

.skill-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 12px;
  padding: 24px;
  background: #f9fafb;
  border-radius: 12px;
  transition: all 0.2s;
}

.skill-item:hover {
  background: #f3f4f6;
  transform: translateY(-4px);
}

.skill-icon {
  width: 72px;
  height: 72px;
  border-radius: 16px;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
}

.skill-icon img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.skill-name {
  font-size: 14px;
  font-weight: 600;
  color: #374151;
}
</style>