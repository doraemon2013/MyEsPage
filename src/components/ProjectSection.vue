<template>
  <section id="projects" class="projects">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title">プロジェクト</h2>
        <a href="#" class="section-link">もっと見る →</a>
      </div>
      <div class="projects-grid">
        <div class="project-card" v-for="project in projects" :key="project.title">
          <div class="project-image">
            <img :src="project.image" :alt="project.title" />
          </div>
          <div class="project-content">
            <h3 class="project-title">{{ project.title }}</h3>
            <div class="project-tags">
              <span class="project-tag" v-for="tag in project.tags" :key="tag">{{ tag }}</span>
            </div>
            <p class="project-description">{{ project.description }}</p>
            <div class="project-actions">
              <button class="project-btn">プロジェクトを見る →</button>
              <button class="project-btn-outline">GitHub</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
const projects = [
  {
    title: "図書管理システム",
    image: "https://neeko-copilot.bytedance.net/api/text2image?prompt=library%20management%20system%20dashboard%20UI%20design%20modern%20clean&image_size=landscape_16_9",
    tags: ["Java", "Spring Boot", "Vue.js", "MySQL", "Redis"],
    description: "図書の貸出・返却・予約・検索・ユーザー管理などの機能を備えたシステムです。"
  },
  {
    title: "レシピ共有サイト",
    image: "https://neeko-copilot.bytedance.net/api/text2image?prompt=cooking%20recipe%20sharing%20website%20UI%20design%20food%20modern&image_size=landscape_16_9",
    tags: ["Vue.js", "TypeScript", "Spring Boot", "MySQL"],
    description: "ユーザーがレシピを投稿・共有・検索できるWebアプリです。コメント機能も実装しました。"
  },
  {
    title: "家計簿アプリ",
    image: "https://neeko-copilot.bytedance.net/api/text2image?prompt=personal%20finance%20budget%20app%20dashboard%20charts%20modern%20UI&image_size=landscape_16_9",
    tags: ["Vue.js", "TypeScript", "MySQL", "Chart.js"],
    description: "日々の収支を記録・分析できる家計簿アプリです。グラフで視覚的に収支を確認できます。"
  }
];
</script>

<style scoped>
.projects {
  padding: 80px 0;
  background: #f9fafb;
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

.projects-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 24px;
}

.project-card {
  background: white;
  border-radius: 16px;
  overflow: hidden;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
  transition: all 0.2s;
}

.project-card:hover {
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.1);
  transform: translateY(-4px);
}

.project-image {
  height: 180px;
  overflow: hidden;
}

.project-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.project-content {
  padding: 20px;
}

.project-title {
  font-size: 18px;
  font-weight: 700;
  color: #1f2937;
  margin: 0 0 12px;
}

.project-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
  margin-bottom: 12px;
}

.project-tag {
  padding: 4px 10px;
  background: #e5e7eb;
  color: #4b5563;
  border-radius: 4px;
  font-size: 11px;
}

.project-description {
  font-size: 13px;
  color: #6b7280;
  line-height: 1.6;
  margin: 0 0 16px;
}

.project-actions {
  display: flex;
  gap: 12px;
}

.project-btn {
  padding: 8px 16px;
  background: #2563eb;
  color: white;
  border: none;
  border-radius: 6px;
  font-size: 12px;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.2s;
}

.project-btn:hover {
  background: #1d4ed8;
}

.project-btn-outline {
  padding: 8px 16px;
  background: none;
  color: #374151;
  border: 1px solid #d1d5db;
  border-radius: 6px;
  font-size: 12px;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.2s;
}

.project-btn-outline:hover {
  background: #f3f4f6;
}
</style>