<template>
  <div class="app">
    <NavBar />
    <main>
      <HeroSection />
      <SkillSection />
      <PersonalQualitySection />
      <ProjectSection />
      <TimelineSection />
      <AboutSection />
    </main>
    <Footer />
  </div>
</template>

<script setup>
import NavBar from './components/NavBar.vue';
import HeroSection from './components/HeroSection.vue';
import SkillSection from './components/SkillSection.vue';
import PersonalQualitySection from './components/PersonalQualitySection.vue';
import ProjectSection from './components/ProjectSection.vue';
import TimelineSection from './components/TimelineSection.vue';
import AboutSection from './components/AboutSection.vue';
import Footer from './components/Footer.vue';
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html {
  scroll-behavior: smooth;
}

body {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

.app {
  min-height: 100vh;
}
</style>