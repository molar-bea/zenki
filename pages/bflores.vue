<template>
  <client-only>
    <NavBar navAdminMode="" />
    
    <div class="bf-container">
      <div class="bf-layout">
        <!-- Sidebar -->
        <aside class="bf-sidebar">
          <div class="bf-profile">
            <img src="/flores.jpg" alt="Raniel John B. Flores" class="bf-profile-img" />
            <h1 class="bf-name">Raniel John B. Flores</h1>
            <p class="bf-role">Web Designer & Full-Stack Developer</p>
          </div>

          <nav class="bf-sidebar-nav">
            <button
              v-for="tab in tabs"
              :key="tab"
              :class="['bf-nav-item', { 'bf-nav-active': currentTab === tab }]"
              @click="currentTab = tab"
            >
              {{ tab }}
            </button>
          </nav>

          <div class="bf-contact-section">
            <h3 class="bf-section-title">Contact</h3>
            <a href="mailto:flores.ranieljohn@gmail.com" class="bf-contact-link">
              <span class="bf-contact-icon">✉</span>
              flores.ranieljohn@gmail.com
            </a>
          </div>
        </aside>

        <!-- Main Content -->
        <main class="bf-main-content">
          <div v-if="currentTab === 'Experience'" class="bf-section">
            <h2>Experience</h2>
            
            <div class="bf-content-item">
              <h3>Assistant Secretary & Event Organizer</h3>
              <p class="bf-institution">Viscan Eruditos (2025–Present)</p>
              <p class="bf-description">Coordinate organizational activities and technical events. Manage logistics, communications, and ensure successful execution of community-driven initiatives and workshops.</p>
            </div>

            <div class="bf-content-item">
              <h3>Start A Ton Finalist</h3>
              <p class="bf-institution">DataCamp x DOST START (2026) </p>
              <p class="bf-description">Recognized as a finalist for developing a data‑driven solution in the education sector. Designed and presented a system that analyzed teacher expertise in science, math, and technology, identifying mismatches in subject mastery and regional distribution. The project highlighted how some regions had an oversupply of qualified teachers while others faced shortages, and proposed an allocation model to optimize deployment. This showcased analytical skills, creativity, and the ability to translate complex educational challenges into actionable, technology‑enabled outcomes.</p>
            </div>

            <div class="bf-content-item">
              <h3>DOST-SEI Scholar's Leadership Camp Participant</h3>
              <p class="bf-institution">Department of Science and Technology (2025)</p>
              <p class="bf-description">Selected participant in an intensive leadership and mentorship program. Developed leadership competencies, built networks with fellow scholars, and gained exposure to emerging technology trends and research.</p>
            </div>

            <div class="bf-content-item">
              <h3>AI For Nature 2025 Participant</h3>
              <p class="bf-institution">Workshop on Artificial Intelligence for Environmental Solutions</p>
              <p class="bf-description">Engaged in hands-on training applying AI techniques to ecological and sustainability problems. Collaborated with peers on projects integrating machine learning with conservation efforts, highlighting the role of technology in advancing environmental stewardship.</p>
            </div>
          </div>

          <div v-if="currentTab === 'Education'" class="bf-section">
            <h2>Education</h2>
            <div class="bf-content-item">
              <h3>B.S. Computer Science</h3>
              <p class="bf-institution">Visayas State University (2024–Present)</p>
              <p class="bf-description">Currently pursuing a degree in Computer Science with a focus on full-stack web development and software engineering principles.</p>
            </div>
            <div class="bf-content-item">
              <h3>DataCamp Scholar</h3>
              <p class="bf-institution">DataCamp Learning Platform</p>
              <p class="bf-description">Selected as a DataCamp Scholar, gaining access to premium data science and programming courses to enhance technical skills.</p>
            </div>
          </div>

          <div v-if="currentTab === 'Skills'" class="bf-section">
            <h2>Skills</h2>
            <div class="bf-content-item">
              <h3>Technical Stack</h3>
              <ul class="bf-skills-list">
                <li>Vue 3 + TypeScript (modular components, props, state)</li>
                <li>Python & SQL (data analysis, machine learning basics)</li>
                <li>Git/GitKraken workflows (branching, PRs, Jira integration)</li>
                <li>UI/UX prototyping (Figma, CSS integration)</li>
                <li>Web Design & Front-end Development</li>
              </ul>
            </div>
          </div>
        </main>
      </div>
    </div>
  </client-only>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { useSeoMeta, useHead } from '@vueuse/head'

const fullName = "Raniel John B. Flores"
const pageTitle = `${fullName} | Personal Page`
const pageDescription = "Resume-style personal page of Raniel John B. Flores, Web Designer and Developer."

useSeoMeta({
  title: () => pageTitle,
  description: () => pageDescription,
  charset: "utf-8",
  viewport: "width=device-width, initial-scale=1.0",
})

useHead({
  link: [
    { rel: "icon", type: "image/png", href: "/logo.png" },
    { rel: "stylesheet", href: "/reset.css" },
    { rel: "stylesheet", href: "/custom.css" },
    { rel: "preconnect", href: "https://fonts.googleapis.com" },
    { rel: "preconnect", href: "https://fonts.gstatic.com", crossorigin: "" },
    {
      rel: "stylesheet",
      href: "https://fonts.googleapis.com/css2?family=DM+Serif+Display:ital@0;1&family=IBM+Plex+Sans:ital,wght@0,100..700;1,100..700&display=swap",
    },
  ],
})

const tabs = ['Experience', 'Education', 'Skills']
const currentTab = ref('Experience')
</script>

<style scoped>
.bf-container {
  min-height: 100vh;
  padding: 2rem;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
}

.bf-portfolio {
  max-width: 1200px;
  margin: 0 auto;
}

.bf-layout {
  display: flex;
  max-width: 1200px;
  margin: 0 auto;
  gap: 0;
  background: white;
  border-radius: 12px;
  overflow: hidden;
  box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
  height: 700px;
}

/* Sidebar Styles */
.bf-sidebar {
  width: 320px;
  background: linear-gradient(135deg, #2c3e50 0%, #34495e 100%);
  padding: 2.5rem 1.5rem;
  color: white;
  display: flex;
  flex-direction: column;
  gap: 2rem;
  flex-shrink: 0;
  overflow: hidden;
}

.bf-profile {
  text-align: center;
}

.bf-profile-img {
  width: 180px;
  height: 180px;
  border-radius: 50%;
  border: 4px solid white;
  object-fit: cover;
  margin-bottom: 1.5rem;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);
}

.bf-name {
  font-size: 1.6rem;
  margin: 0 0 0.5rem 0;
  font-weight: 700;
  color: white;
}

.bf-role {
  font-size: 0.95rem;
  color: #ecf0f1;
  margin: 0;
  font-weight: 500;
}

.bf-sidebar-nav {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.bf-nav-item {
  padding: 1rem 1.2rem;
  background: rgba(255, 255, 255, 0.1);
  border: 2px solid transparent;
  border-radius: 6px;
  color: #ecf0f1;
  cursor: pointer;
  font-weight: 600;
  font-size: 0.95rem;
  transition: all 0.3s ease;
  text-align: left;
}

.bf-nav-item:hover {
  background: rgba(255, 255, 255, 0.2);
  border-color: #667eea;
}

.bf-nav-active {
  background: #667eea;
  border-color: #667eea;
  color: white;
}

.bf-contact-section {
  border-top: 1px solid rgba(255, 255, 255, 0.2);
  padding-top: 1.5rem;
}

.bf-section-title {
  font-size: 0.9rem;
  text-transform: uppercase;
  letter-spacing: 1px;
  color: #bdc3c7;
  margin: 0 0 1rem 0;
  font-weight: 700;
}

/* Main Content Styles */
.bf-main-content {
  flex: 1;
  padding: 3rem;
  overflow-y: auto;
  overflow-x: hidden;
}

.bf-section h2 {
  color: #2c3e50;
  font-size: 2rem;
  margin: 0 0 2rem 0;
  font-weight: 700;
  border-bottom: 3px solid #667eea;
  padding-bottom: 0.75rem;
}

.bf-content-item {
  margin-bottom: 2.5rem;
  padding-bottom: 2rem;
  border-bottom: 1px solid #ecf0f1;
}

.bf-content-item:last-child {
  border-bottom: none;
  padding-bottom: 0;
  margin-bottom: 0;
}

.bf-content-item h3 {
  color: #667eea;
  font-size: 1.3rem;
  margin: 0 0 0.5rem 0;
  font-weight: 700;
}

.bf-institution {
  color: #7f8c8d;
  font-size: 0.95rem;
  margin: 0.3rem 0 0.8rem 0;
  font-weight: 600;
}

.bf-description {
  color: #555;
  line-height: 1.8;
  margin: 0;
  font-size: 0.95rem;
}

.bf-contact-link {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  color: #ecf0f1;
  text-decoration: none;
  font-size: 0.9rem;
  transition: all 0.3s ease;
  word-break: break-all;
}

.bf-contact-link:hover {
  color: #667eea;
  margin-left: 0.25rem;
}

.bf-contact-icon {
  font-size: 1.2rem;
  flex-shrink: 0;
}

.bf-tab-content ul {
  list-style: none;
  padding: 0;
  margin: 1rem 0 0 0;
}

.bf-tab-content li {
  padding: 0.6rem 0;
  color: #555;
  line-height: 1.6;
  font-size: 0.95rem;
  border-bottom: 1px solid #ecf0f1;
}

.bf-tab-content li:last-child {
  border-bottom: none;
}

.bf-skills-list {
  list-style: none;
  padding: 0;
  margin: 1rem 0 0 0;
}

.bf-skills-list li {
  padding: 0.6rem 0;
  color: #555;
  line-height: 1.6;
  font-size: 0.95rem;
  border-bottom: 1px solid #ecf0f1;
}

.bf-skills-list li:last-child {
  border-bottom: none;
}

/* Responsive Design */
@media (max-width: 768px) {
  .bf-layout {
    flex-direction: column;
    gap: 0;
  }

  .bf-sidebar {
    width: 100%;
    padding: 2rem 1.5rem;
  }

  .bf-main-content {
    padding: 2rem;
  }

  .bf-sidebar-nav {
    flex-direction: row;
    flex-wrap: wrap;
  }

  .bf-nav-item {
    flex: 1;
    min-width: 120px;
  }
}
</style>
