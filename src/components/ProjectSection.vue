<template>
  <section id="projects" class="projects">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title">{{ projectData.section_title }}</h2>
        <a :href="projectData.more_link" class="section-link" target="_blank" rel="noopener noreferrer">もっと見る →</a>
      </div>
      <div class="projects-grid">
        <div class="project-card" v-for="project in projectData.projects" :key="project.title">
          <div class="project-thumbnail">
            <img :src="project.thumbnail_url" :alt="project.title" />
          </div>
          <div class="project-content">
            <h3 class="project-title">{{ project.title }}</h3>
            <div class="project-tags">
              <span class="tag" v-for="tag in project.tags" :key="tag">{{ tag }}</span>
            </div>
            <p class="project-description">{{ project.description }}</p>
            <div class="project-links">
              <a :href="project.links.project_url" class="project-link" target="_blank" rel="noopener noreferrer">プロジェクトを見る</a>
              <a :href="project.links.github_url" class="github-link" target="_blank" rel="noopener noreferrer">
                <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor">
                  <path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"/>
                </svg>
              </a>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const projectData = ref({
  section_title: 'プロジェクト',
  more_link: '/projects',
  projects: []
});

const jsonModules = import.meta.glob('../json/*.json', { eager: true });

onMounted(() => {
  if (jsonModules['../json/projects.json']) {
    projectData.value = jsonModules['../json/projects.json'].default;
  }
});
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
  grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
  gap: 32px;
  grid-auto-rows: 1fr;
}

.project-card {
  background: white;
  border-radius: 12px;
  overflow: hidden;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
  transition: all 0.2s;
  display: flex;
  flex-direction: column;
}

.project-card:hover {
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
  transform: translateY(-4px);
}

.project-thumbnail {
  width: 100%;
  height: 200px;
  overflow: hidden;
  background: #e5e7eb;
}

.project-thumbnail img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.project-content {
  padding: 24px;
  flex: 1;
  display: flex;
  flex-direction: column;
}

.project-description {
  flex: 1;
}

.project-title {
  font-size: 18px;
  font-weight: 600;
  color: #1f2937;
  margin: 0 0 12px 0;
}

.project-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  margin-bottom: 12px;
}

.tag {
  padding: 4px 12px;
  background: #dbeafe;
  color: #1e40af;
  font-size: 12px;
  font-weight: 500;
  border-radius: 9999px;
}

.project-description {
  font-size: 14px;
  color: #6b7280;
  line-height: 1.6;
  margin: 0 0 16px 0;
}

.project-links {
  display: flex;
  gap: 12px;
}

.project-link {
  padding: 8px 16px;
  background: #2563eb;
  color: white;
  text-decoration: none;
  font-size: 14px;
  font-weight: 500;
  border-radius: 6px;
  transition: background 0.2s;
}

.project-link:hover {
  background: #1d4ed8;
}

.github-link {
  padding: 8px;
  background: #f3f4f6;
  color: #374151;
  border-radius: 6px;
  transition: all 0.2s;
}

.github-link:hover {
  background: #e5e7eb;
  color: #1f2937;
}
</style>