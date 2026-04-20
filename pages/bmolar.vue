<script setup lang="ts">
import { ref } from "vue";
import { useSeoMeta, useHead } from "@vueuse/head";

const pageTitle = "Bea Molar";
const pageDescription = "The personal page of Bea Molar.";

useSeoMeta({
  title: () => pageTitle,
  description: () => pageDescription,
});

useHead({
  link: [
    { rel: "preconnect", href: "https://fonts.googleapis.com" },
    { rel: "preconnect", href: "https://fonts.gstatic.com", crossorigin: "" },
    { rel: "stylesheet", href: "https://fonts.googleapis.com/css2?family=IBM+Plex+Sans:wght@300;400;600;700&display=swap" },
  ],
  style: [
    { innerHTML: 'body { margin: 0; overflow: hidden; }' } 
  ]
});


const activeSection = ref("projects");

const navItems = [
  { id: "projects", label: "Projects" },
  { id: "experience", label: "Experience" },
  { id: "contacts", label: "Contacts" }
];

const setSection = (id: string) => {
  activeSection.value = id;
};

</script>

<template>
  <client-only>
    <div class="portfolio-layout">
      <aside class="sidebar">
        
        <div class="sidebar-content-wrapper">
          <div class="header-section">
            <div class="profile-avatar">
              <img src="/public/molar.jpg" alt="Bea Molar" class="profile-img" />
            </div>

            <h1 class="name">Bea Molar</h1>
            <h2 class="title">JUNIOR SOFTWARE DEVELOPER</h2>
            <p class="description">
              I am a junior software developer learning the different fields in computing, currently studying Bachelor of Science in Computer Science at Visayas State University.
            </p>
          </div>

          <nav class="timeline-nav">
            <div class="timeline-line"></div>
            <div 
              v-for="item in navItems" 
              :key="item.id" 
              class="nav-node"
              @click="setSection(item.id)"
              :class="{ 'is-active': activeSection === item.id }"
            >
              <div class="node-content">
                <span v-if="activeSection === item.id" class="node-label">
                  {{ item.label }}
                </span>
              </div>
            </div>
          </nav>
        </div>
      </aside>

      <main class="main-content">
        
        <div v-if="activeSection === 'experience'" class="content-view">
          <div class="resume-list">
            <div class="resume-card">
              <div class="resume-header">
                <h3 class="resume-title">Part-time Associate</h3>
                <span class="resume-org">MUNICIPAL PLANNING AND DEVELOPMENT OFFICE (MPDO)</span>
                <span class="resume-date">June 18 – July 18, 2024</span>
              </div>
              <ul class="resume-bullets">
                <li>Acquired practical experience with office tools and software applications used by the organization.</li>
                <li>Assisted in managing server systems and databases that processed data for 51 municipal barangays to facilitate office operations and data management.</li>
                <li>Utilized mapping software and other specialized tools in support of municipal planning and development projects.</li>
              </ul>
            </div>
          </div>
        </div>

        <div v-if="activeSection === 'projects'" class="content-view">
          <div class="resume-list">
            
            <div class="resume-card">
              <div class="resume-header">
                <h3 class="resume-title">Neighborhood</h3>
                <span class="resume-org">Lead Developer</span>
                <span class="resume-date">October - December 2025</span>
              </div>
              <ul class="resume-bullets">
                <li>Developed a high-performance local directory hub using TypeScript, React, and Next.js, enabling users to discover and review small businesses within their immediate vicinity.</li>
                <li>Architected a scalable backend using Supabase for real-time data management and user authentication, ensuring seamless role-based access for both customers and sellers.</li>
                <li>Integrated React Leaflet for dynamic geospatial mapping, reducing location-search latency by 30% and enhancing user proximity visualization.</li>
              </ul>
            </div>

            <div class="resume-card">
              <div class="resume-header">
                <h3 class="resume-title">Building Classifier</h3>
                <span class="resume-org">Developer</span>
                <span class="resume-date">May 2025</span>
              </div>
              <ul class="resume-bullets">
                <li>Built a mobile building classifier using Kotlin that identifies 10 organizational units at Visayas State University with high recognition accuracy.</li>
                <li>Leveraged TensorFlow and advanced image processing to train a custom model on a dataset of 1000+ building images, automating the retrieval of department info.</li>
                <li>Optimized the classification algorithm to process visual data in under 2 seconds, improving search speed by 40% compared to manual directory lookups.</li>
              </ul>
            </div>

            <div class="resume-card">
              <div class="resume-header">
                <h3 class="resume-title">VersaTula</h3>
                <span class="resume-org">Developer & UI/UX Designer</span>
                <span class="resume-date">November – December 13, 2024</span>
              </div>
              <ul class="resume-bullets">
                <li>Developed "VersaTula," a language classification game processing 10,000+ text inputs using a Feedforward Neural Network (FFNN) model with high accuracy.</li>
                <li>Leveraged Python for implementing the machine learning model and C# with Windows Forms for the user interface.</li>
              </ul>
            </div>

            <div class="resume-card">
              <div class="resume-header">
                <h3 class="resume-title">STUDIUUS</h3>
                <span class="resume-org">Developer</span>
                <span class="resume-date">May 2024</span>
              </div>
              <ul class="resume-bullets">
                <li>Created Studiuus, a comprehensive flashcard application designed to handle thousands of data points to enhance student study practices by 20%.</li>
                <li>Utilized PHP and C# for application development, incorporating effective database management techniques to ensure a robust user experience.</li>
              </ul>
            </div>

          </div>
        </div>

        <div v-if="activeSection === 'contacts'" class="content-view">
          <div class="contact-grid">
            <h2 class="view-title-alt">Let's Connect</h2>
            <p class="contact-desc">Feel free to reach out for collaborations or just a friendly chat about tech and design.</p>
            
            <div class="contact-links-container">
              <a href="https://www.linkedin.com/in/bea-molar/" target="_blank" class="contact-card">
                <div class="contact-icon">
                  <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5"><path d="M16 8a6 6 0 0 1 6 6v7h-4v-7a2 2 0 0 0-2-2 2 2 0 0 0-2 2v7h-4v-7a6 6 0 0 1 6-6z"></path><rect x="2" y="9" width="4" height="12"></rect><circle cx="4" cy="4" r="2"></circle></svg>
                </div>
                <div class="contact-info">
                  <span class="contact-label">LinkedIn</span>
                  <span class="contact-handle">Bea Molar</span>
                </div>
              </a>

              <a href="https://github.com/molar-bea" target="_blank" class="contact-card">
                <div class="contact-icon">
                  <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5"><path d="M9 19c-5 1.5-5-2.5-7-3m14 6v-3.87a3.37 3.37 0 0 0-.94-2.61c3.14-.35 6.44-1.54 6.44-7A5.44 5.44 0 0 0 20 4.77 5.07 5.07 0 0 0 19.91 1S18.73.65 16 2.48a13.38 13.38 0 0 0-7 0C6.27.65 5.09 1 5.09 1A5.07 5.07 0 0 0 5 4.77a5.44 5.44 0 0 0-1.5 3.78c0 5.42 3.3 6.61 6.44 7A3.37 3.37 0 0 0 9 18.13V22"></path></svg>
                </div>
                <div class="contact-info">
                  <span class="contact-label">GitHub</span>
                  <span class="contact-handle">molar-bea</span>
                </div>
              </a>

              <a href="mailto:22-1-00410@vsu.edu.ph" class="contact-card">
                <div class="contact-icon">
                  <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5"><path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"></path><polyline points="22,6 12,13 2,6"></polyline></svg>
                </div>
                <div class="contact-info">
                  <span class="contact-label">Email</span>
                  <span class="contact-handle">Bea Molar</span>
                </div>
              </a>

              <a href="https://www.facebook.com/beamolar05131/" target="_blank" class="contact-card">
                <div class="contact-icon">
                  <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5"><path d="M18 2h-3a5 5 0 0 0-5 5v3H7v4h3v8h4v-8h3l1-4h-4V7a1 1 0 0 1 1-1h3z"></path></svg>
                </div>
                <div class="contact-info">
                  <span class="contact-label">Facebook</span>
                  <span class="contact-handle">Bea Molar</span>
                </div>
              </a>
            </div>
          </div>
      
        </div>
      </main>

    </div>
  </client-only>
</template>

<style scoped>
/* Base Layout */
.portfolio-layout {
  display: flex;
  height: 100vh; 
  overflow: hidden; 
  font-family: "IBM Plex Sans", sans-serif;
  color: #ffffff;
  background-color: #0b0a0e;
}

/* Left Sidebar */
.sidebar {
  width: 45%;
  max-width: 550px;
  min-width: 400px;
  height: 100vh; 
  background-color: #050406;
  overflow: hidden; 
}

/* Inner wrapper for sidebar content to manage spacing */
.sidebar-content-wrapper {
  padding: 50px 80px;
  display: flex;
  flex-direction: column;
  height: 100%; 
  justify-content: space-between;
  box-sizing: border-box;
}

/* Right Main Content*/
.main-content {
  flex: 1;
  height: 100%;
  overflow-y: auto; 
  background-color: #1c1a22;
  padding: 80px 60px;
  scroll-behavior: smooth;
  box-sizing: border-box;
}

/* Header Info */
.header-section {
  margin-bottom: 40px;
}

/* Profile Picture */
.profile-avatar {
  margin-bottom: 24px;
}

.profile-img {
  width: 96px;
  height: 96px;
  border-radius: 50%;
  object-fit: cover;
  
  border: 2px solid #4a4555; 
  padding: 4px;
  background-color: #050406;
  transition: border-color 0.3s ease, transform 0.3s ease;
}

.profile-img:hover {
  
  border-color: #b5a4cb; 
  transform: scale(1.05);
}

.name {
  font-size: 2.5rem;
  font-weight: 700;
  margin: 0 0 5px 0;
  letter-spacing: -0.5px;
}

.title {
  font-size: 0.9rem;
  font-weight: 400;
  color: #d1d1d1;
  letter-spacing: 1px;
  margin: 0 0 30px 0;
}

.description {
  font-size: 0.95rem;
  line-height: 1.7;
  color: #a0a0a0;
}


.view-title-alt {
  font-size: 2.5rem;
  font-weight: 700;
  margin-bottom: 10px;
  color: #ffffff;
}

.contact-desc {
  color: #a0a0a0;
  font-size: 1.1rem;
  margin-bottom: 40px;
  max-width: 500px;
}

.contact-links-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
  gap: 20px;
}

.contact-card {
  display: flex;
  align-items: center;
  gap: 20px;
  background-color: rgba(255, 255, 255, 0.02);
  border: 1px solid rgba(255, 255, 255, 0.05);
  border-radius: 12px;
  padding: 20px;
  text-decoration: none;
  transition: all 0.3s ease;
}

.contact-card:hover {
  background-color: rgba(255, 255, 255, 0.05);
  border-color: #b5a4cb;
  transform: translateX(5px);
}

.contact-icon {
  width: 40px;
  height: 40px;
  color: #b5a4cb;
  display: flex;
  align-items: center;
  justify-content: center;
}

.contact-icon svg {
  width: 100%;
  height: 100%;
}

.contact-info {
  display: flex;
  flex-direction: column;
}

.contact-label {
  font-size: 0.8rem;
  text-transform: uppercase;
  letter-spacing: 1px;
  color: #888888;
}

.contact-handle {
  font-size: 1rem;
  font-weight: 600;
  color: #ffffff;
}

/* Timeline Navigation */
.timeline-nav {
  position: relative;
  display: flex;
  flex-direction: column;
  gap: 40px;
  margin: 40px 0;
  padding-left: 20px;
}

.timeline-line {
  position: absolute;
  left: 31.5px;
  top: 10px;
  bottom: 10px;
  width: 1px;
  background-color: #4a4555;
  z-index: 1;
}

.nav-node {
  position: relative;
  display: flex;
  align-items: center;
  z-index: 2;
  cursor: pointer;
  height: 36px;
}

.node-content {
  width: 24px;
  height: 24px;
  border-radius: 20px;
  background-color: #b5a4cb; 
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  display: flex;
  align-items: center;
  justify-content: flex-start;
}

.nav-node:hover:not(.is-active) .node-content {
  transform: scale(1.15);
}

.nav-node.is-active .node-content {
  width: 140px;
  height: 36px;
  margin-left: -6px; 
  padding-left: 35px; 
}

.node-label {
  color: #000000;
  font-weight: 600;
  font-size: 0.95rem;
  white-space: nowrap;
  animation: fadeInLabel 0.2s ease forwards;
  animation-delay: 0.1s;
  opacity: 0;
}

@keyframes fadeInLabel {
  from { opacity: 0; }
  to { opacity: 1; }
}

/* Content Views */
.content-view {
  width: 100%;
  max-width: 800px;
  margin: 0 auto;
  animation: fadeIn 0.4s ease forwards;
}

.empty-view {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100%;
  text-align: center;
}

.view-title {
  font-size: 2rem;
  font-weight: 600;
  line-height: 1.4;
  color: #a0a0a0;
}

/* Beautiful Resume Cards */
.resume-list {
  display: flex;
  flex-direction: column;
  gap: 30px;
  padding-bottom: 40px; 
}

.resume-card {
  background-color: rgba(255, 255, 255, 0.02);
  border: 1px solid rgba(255, 255, 255, 0.05);
  border-radius: 16px;
  padding: 30px;
  transition: transform 0.3s ease, background-color 0.3s ease, box-shadow 0.3s ease;
}

.resume-card:hover {
  background-color: rgba(255, 255, 255, 0.04);
  transform: translateY(-4px);
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
}

.resume-header {
  display: flex;
  flex-direction: column;
  gap: 6px;
  margin-bottom: 20px;
}

.resume-title {
  font-size: 1.4rem;
  font-weight: 600;
  color: #ffffff;
  margin: 0;
}

.resume-org {
  font-size: 1rem;
  color: #d7c9eb;
  font-weight: 500;
}

.resume-date {
  font-size: 0.85rem;
  color: #888888;
  font-weight: 400;
  letter-spacing: 0.5px;
  text-transform: uppercase;
}

.resume-bullets {
  list-style-type: none;
  padding: 0;
  margin: 0;
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.resume-bullets li {
  position: relative;
  padding-left: 24px;
  color: #b3b3b3;
  font-size: 0.95rem;
  line-height: 1.6;
}

.resume-bullets li::before {
  content: "▹";
  position: absolute;
  left: 0;
  top: 0;
  color: #b5a4cb;
  font-size: 1.2rem;
  line-height: 1.4;
}

@keyframes fadeIn {
  from { opacity: 0; transform: translateY(10px); }
  to { opacity: 1; transform: translateY(0); }
}

/* Responsive */
@media (max-width: 900px) {
  .portfolio-layout {
    flex-direction: column;
    height: auto;
    overflow: auto; 
  }
  
  .sidebar {
    width: 100%;
    max-width: none;
    min-width: 0;
    height: auto;
    overflow: visible;
  }

  .sidebar-content-wrapper {
    padding: 40px;
  }

  .main-content {
    height: auto;
    overflow: visible;
    padding: 40px;
  }

}
</style>