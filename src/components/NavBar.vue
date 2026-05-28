<template>
  <nav class="navbar">
    <div class="container">
      <div class="navbar-brand">
        <div class="logo">
          <svg width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <path d="M12 2L2 7l10 5 10-5-10-5zM2 17l10 5 10-5M2 12l10 5 10-5"/>
          </svg>
          <span class="brand-text">
            <span class="brand-name">練潮田</span>
            <span class="brand-title">Webエンジニア</span>
          </span>
        </div>
      </div>
      <div class="navbar-menu">
        <ul class="nav-links">
          <li><a href="#" :class="{ active: activeNav === 'home' }" @click.prevent="scrollToSection('home')">ホーム</a></li>
          <li><a href="#skills" :class="{ active: activeNav === 'skills' }" @click.prevent="scrollToSection('skills')">スキル</a></li>
          <li><a href="#projects" :class="{ active: activeNav === 'projects' }" @click.prevent="scrollToSection('projects')">プロジェクト</a></li>
          <li><a href="#timeline" :class="{ active: activeNav === 'timeline' }" @click.prevent="scrollToSection('timeline')">学習記録</a></li>
          <li><a href="#about" :class="{ active: activeNav === 'about' }" @click.prevent="scrollToSection('about')">自己紹介</a></li>
          <li><a href="#contact" :class="{ active: activeNav === 'contact' }" @click.prevent="scrollToSection('contact')">連絡先</a></li>
        </ul>
        <div class="nav-right">
          <button class="lang-btn">日本語</button>
          <button class="theme-toggle">
            <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <circle cx="12" cy="12" r="5"/>
              <line x1="12" y1="1" x2="12" y2="3"/>
              <line x1="12" y1="21" x2="12" y2="23"/>
              <line x1="4.22" y1="4.22" x2="5.64" y2="5.64"/>
              <line x1="18.36" y1="18.36" x2="19.78" y2="19.78"/>
              <line x1="1" y1="12" x2="3" y2="12"/>
              <line x1="21" y1="12" x2="23" y2="12"/>
              <line x1="4.22" y1="19.78" x2="5.64" y2="18.36"/>
              <line x1="18.36" y1="5.64" x2="19.78" y2="4.22"/>
            </svg>
          </button>
        </div>
      </div>
    </div>
  </nav>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

const activeNav = ref('home');

const sections = [
  { id: 'home', selector: 'section.hero' },
  { id: 'skills', selector: 'section#skills' },
  { id: 'projects', selector: 'section#projects' },
  { id: 'timeline', selector: 'section#timeline' },
  { id: 'about', selector: 'section#about' },
  { id: 'contact', selector: 'section#about' }
];

const scrollToSection = (id) => {
  if (id === 'home') {
    window.scrollTo({ top: 0, behavior: 'smooth' });
  } else {
    const element = document.querySelector(`#${id}`);
    if (element) {
      element.scrollIntoView({ behavior: 'smooth' });
    }
  }
};

const handleScroll = () => {
  const scrollPosition = window.scrollY + 150;
  
  for (let i = sections.length - 1; i >= 0; i--) {
    const section = sections[i];
    const element = document.querySelector(section.selector);
    if (element) {
      const offsetTop = element.offsetTop;
      if (scrollPosition >= offsetTop) {
        activeNav.value = section.id;
        break;
      }
    }
  }
};

onMounted(() => {
  window.addEventListener('scroll', handleScroll, { passive: true });
});

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll);
});
</script>

<style scoped>
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  background: rgba(255, 255, 255, 0.95);
  backdrop-filter: blur(10px);
  border-bottom: 1px solid #e5e7eb;
  z-index: 100;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 24px;
}

.navbar-brand {
  display: flex;
  align-items: center;
}

.logo {
  display: flex;
  align-items: center;
  gap: 12px;
  color: #2563eb;
}

.brand-text {
  display: flex;
  flex-direction: column;
}

.brand-name {
  font-weight: 700;
  font-size: 16px;
  color: #1f2937;
}

.brand-title {
  font-size: 12px;
  color: #6b7280;
}

.navbar-menu {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.nav-links {
  display: flex;
  gap: 32px;
  list-style: none;
  padding: 0;
  margin: 0;
}

.nav-links a {
  text-decoration: none;
  color: #374151;
  font-size: 14px;
  font-weight: 500;
  transition: color 0.2s;
}

.nav-links a:hover,
.nav-links a.active {
  color: #2563eb;
}

.nav-right {
  display: flex;
  align-items: center;
  gap: 16px;
  margin-left: 32px;
}

.lang-btn {
  padding: 6px 12px;
  background: #f3f4f6;
  border: 1px solid #d1d5db;
  border-radius: 6px;
  font-size: 12px;
  cursor: pointer;
  transition: all 0.2s;
}

.lang-btn:hover {
  background: #e5e7eb;
}

.theme-toggle {
  background: none;
  border: none;
  color: #6b7280;
  cursor: pointer;
  padding: 6px;
  border-radius: 6px;
  transition: all 0.2s;
}

.theme-toggle:hover {
  background: #f3f4f6;
  color: #374151;
}

.navbar {
  display: flex;
  align-items: center;
  height: 64px;
}

.navbar .container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
}
</style>