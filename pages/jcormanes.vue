<script lang="ts"></script>

<template>
  <client-only>
    <NavBar navAdminMode="" />
    <div id="zkMain" class="zk-main">
      <div class="portfolio-container">
        
        <header class="hero-card">
          <div class="profile-frame">
            <img src="/cormanes.jpg" alt="Jo Mari Jess Cormanes" class="profile-pic" />
          </div>
          <div class="hero-text">
            <h1>Jo Mari Jess Cormanes</h1>
            <p class="tagline">Aspiring Junior Developer</p>
            <div class="contact-bar">
              <a href="mailto:jesscormanes@gmail.com" class="contact-link">Email</a>
              <a href="https://github.com/Cormz12-26" target="_blank" class="contact-link">GitHub</a>
              <span class="phone">+63 920 458 1195</span>
            </div>
          </div>
        </header>

        <main class="portfolio-grid">
          
          <div class="column">
            <section class="card">
              <h2 class="section-title">Education</h2>
              <div class="education-item">
                <p class="institution">Visayas State University</p>
                <p class="degree">BS Computer Science</p>
                <p class="years">2024 — Present</p>
              </div>
            </section>

            <section class="card">
              <h2 class="section-title">Technical Skills</h2>
              <div class="skills-wrap">
                <div class="skill-group">
                  <span class="label">Languages</span>
                  <p>C++, x86 Assembly, TypeScript, SQL</p>
                </div>
                <div class="skill-group">
                  <span class="label">Frameworks</span>
                  <p>Vue 3, Nuxt, Node.js</p>
                </div>
                <div class="skill-group">
                  <span class="label">Tools</span>
                  <p>Code::Blocks, MySQL, Git</p>
                </div>
              </div>
            </section>
          </div>

          <div class="column">
            <section class="card project-card">
              <h2 class="section-title">Featured Project</h2>
              <div class="project-header">
                <h3>Zenki | Admission Guide App</h3>
                <span class="badge">In Progress</span>
              </div>
              <p class="project-desc">
                A comprehensive tracking system for university applicants. Built with Nuxt and Vue, 
                focusing on DPA and GDPR compliance to ensure secure handling of student data.
              </p>
              <div class="tech-stack">
              </div>
            </section>

            <section class="card project-card">
              <h2 class="section-title">Other Work</h2>
              <div class="project-header">
                <h3>Database Integration</h3>
              </div>
              <p class="project-desc">
                Developed backend architectures using C++ and MySQL, implementing efficient data 
                retrieval and management systems within Code::Blocks environments.
              </p>
            </section>
          </div>

        </main>
      </div>
    </div>
    <Copyright />
  </client-only>
</template>

<script setup lang="ts">
import { useSeoMeta, useHead } from "@vueuse/head";

const title = "Jo Mari Jess Cormanes | Portfolio";
const description = "Professional portfolio of Jo Mari Jess Cormanes, a Computer Science student at VSU.";

useSeoMeta({
  title: () => title,
  description: () => description,
  charset: "utf-8",
  viewport: "width=device-width, initial-scale=1.0",
});

useHead({
  link: [
    { rel: "icon", type: "image/png", href: "/logo.png" },
    { rel: "stylesheet", href: "/reset.css" },
    { rel: "stylesheet", href: "/custom.css" },
    { rel: "preconnect", href: "https://fonts.googleapis.com" },
    { rel: "preconnect", href: "https://fonts.gstatic.com", crossorigin: "" },
    { rel: "stylesheet", href: "https://fonts.googleapis.com/css2?family=DM+Serif+Display:ital@0;1&family=IBM+Plex+Sans:ital,wght@0,100..700;1,100..700&display=swap" },
  ],
});
</script>

<style scoped>
.zk-main {
  padding: 60px 20px;
  background-color: #f8f9fa;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  font-family: 'IBM Plex Sans', sans-serif;
}

.portfolio-container {
  max-width: 1000px;
  width: 100%;
}

.hero-card {
  background: #ffffff;
  padding: 40px;
  border-radius: 20px;
  display: flex;
  align-items: center;
  gap: 40px;
  margin-bottom: 30px;
  box-shadow: 0 10px 30px rgba(0,0,0,0.05);
}

/* Lime Border Logic */
.profile-pic {
  width: 160px;
  height: 160px;
  border-radius: 50%;
  object-fit: cover;
  border: 6px solid #32CD32; /* Lime Green Border */
  padding: 4px;
  background-color: white; /* Ensures white gap between photo and lime border */
  box-shadow: 0 4px 15px rgba(50, 205, 50, 0.2); /* Subtle lime glow */
}

h1 {
  font-family: 'DM Serif Display', serif;
  font-size: 3rem;
  line-height: 1.1;
  margin-bottom: 10px;
}

.tagline {
  font-size: 1.1rem;
  color: #666;
  text-transform: uppercase;
  letter-spacing: 1.5px;
  margin-bottom: 20px;
}

.contact-bar {
  display: flex;
  gap: 20px;
  font-size: 0.9rem;
}

.contact-link {
  color: #1a1a1a;
  font-weight: 600;
  text-decoration: none;
  border-bottom: 2px solid #eee;
}

.contact-link:hover {
  border-bottom-color: #32CD32; /* Hover matches lime border */
}

.portfolio-grid {
  display: grid;
  grid-template-columns: 1fr 1.5fr;
  gap: 30px;
}

.column {
  display: flex;
  flex-direction: column;
  gap: 30px;
}

.card {
  background: white;
  padding: 30px;
  border-radius: 20px;
  box-shadow: 0 4px 15px rgba(0,0,0,0.03);
}

.section-title {
  font-family: 'DM Serif Display', serif;
  font-size: 1.5rem;
  margin-bottom: 20px;
  color: #1a1a1a;
  border-left: 4px solid #32CD32; /* Lime accent for section titles */
  padding-left: 15px;
}

/* Rest of the styling remains consistent... */
.institution { font-weight: 700; font-size: 1.1rem; }
.degree { color: #555; margin: 5px 0; }
.years { font-size: 0.85rem; color: #999; }
.skill-group { margin-bottom: 15px; }
.label { display: block; font-size: 0.75rem; text-transform: uppercase; color: #aaa; letter-spacing: 1px; font-weight: 700; }
.project-header { display: flex; justify-content: space-between; align-items: flex-start; margin-bottom: 10px; }
.project-header h3 { font-weight: 700; font-size: 1.2rem; }
.badge { font-size: 0.7rem; background: #f0f0f0; padding: 4px 10px; border-radius: 20px; font-weight: 600; }
.project-desc { font-size: 0.95rem; line-height: 1.6; color: #444; }
.tech-stack { margin-top: 15px; display: flex; gap: 10px; font-size: 0.8rem; color: #32CD32; font-weight: 600; }

@media (max-width: 850px) {
  .hero-card { flex-direction: column; text-align: center; }
  .portfolio-grid { grid-template-columns: 1fr; }
  .contact-bar { justify-content: center; }
}
</style>