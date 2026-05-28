<template>
  <section id="skills" class="skills">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title">スキル</h2>
        <a href="#" class="section-link">もっと見る →</a>
      </div>
      <div class="skills-grid">
        <div class="skill-item" v-for="skill in skills" :key="skill.name">
          <div class="skill-icon" :style="{ background: skill.bgColor }">
            <img :src="skill.icon" :alt="skill.name" />
          </div>
          <div class="skill-name">{{ skill.name }}</div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
const skills = [
  { name: "Java", icon: "https://neeko-copilot.bytedance.net/api/text2image?prompt=Java%20programming%20language%20logo%20orange%20cup%20simple%20icon&image_size=square", bgColor: "#f87171" },
  { name: "Spring Boot", icon: "https://neeko-copilot.bytedance.net/api/text2image?prompt=Spring%20Boot%20framework%20logo%20green%20leaf%20simple%20icon&image_size=square", bgColor: "#4ade80" },
  { name: "Vue.js", icon: "https://neeko-copilot.bytedance.net/api/text2image?prompt=Vue.js%20framework%20logo%20green%20V%20letter%20simple%20icon&image_size=square", bgColor: "#4ade80" },
  { name: "MySQL", icon: "https://neeko-copilot.bytedance.net/api/text2image?prompt=MySQL%20database%20logo%20orange%20dolphin%20simple%20icon&image_size=square", bgColor: "#fb923c" },
  { name: "Redis", icon: "https://neeko-copilot.bytedance.net/api/text2image?prompt=Redis%20database%20logo%20red%20circle%20simple%20icon&image_size=square", bgColor: "#ef4444" },
  { name: "Docker", icon: "https://neeko-copilot.bytedance.net/api/text2image?prompt=Docker%20container%20logo%20blue%20whale%20simple%20icon&image_size=square", bgColor: "#3b82f6" },
  { name: "HTML5", icon: "https://neeko-copilot.bytedance.net/api/text2image?prompt=HTML5%20logo%20orange%20shield%20simple%20icon&image_size=square", bgColor: "#fb923c" },
  { name: "CSS3", icon: "https://neeko-copilot.bytedance.net/api/text2image?prompt=CSS3%20logo%20blue%20shield%20simple%20icon&image_size=square", bgColor: "#3b82f6" },
  { name: "JavaScript", icon: "https://neeko-copilot.bytedance.net/api/text2image?prompt=JavaScript%20logo%20yellow%20shield%20simple%20icon&image_size=square", bgColor: "#fbbf24" },
  { name: "TypeScript", icon: "https://neeko-copilot.bytedance.net/api/text2image?prompt=TypeScript%20logo%20blue%20TS%20letter%20simple%20icon&image_size=square", bgColor: "#3b82f6" },
];
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
  grid-template-columns: repeat(5, 1fr);
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
  width: 40px;
  height: 40px;
  object-fit: contain;
  filter: brightness(0) invert(1);
}

.skill-name {
  font-size: 14px;
  font-weight: 600;
  color: #374151;
}
</style>