<script setup>
import { ref } from 'vue'

const activeTab = ref('home')

const navLinks = [
  { id: 'home', label: 'Home', icon: 'M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6' },
  { id: 'experience', label: 'Experience & Projects', icon: 'M21 13.255A23.931 23.931 0 0112 15c-3.183 0-6.22-.62-9-1.745M16 6V4a2 2 0 00-2-2h-4a2 2 0 00-2 2v2m4 6h.01M5 20h14a2 2 0 002-2V8a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z' },
  { id: 'contact', label: 'Contact', icon: 'M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z' }
]

const experiences = [
  {
    title: 'Education Committee Head',
    role: 'Mabolo Men’s Home',
    desc: 'Led educational initiatives and support programs for the community from 2025 to present.'
  },
  {
    title: 'Editor in Chief',
    role: 'The Bato Angler',
    desc: 'Managed publication operations, editorial decisions, and team coordination (2023-2024).'
  },
  {
    title: 'StoryaViscans',
    role: 'Full-Stack Developer',
    desc: 'Developed a community-based forum platform designed to connect university students.'
  },
  {
    title: 'NourishDesk',
    role: 'C# Developer',
    desc: 'Built a desktop application with robust features for donation management.'
  },
  {
    title: 'Anklet Sensor for the Blind',
    role: 'Hardware/Software Integration',
    desc: 'Created a capstone project utilizing Arduino and ultrasonic sensors for obstacle detection.'
  },
  {
    title: 'Opti',
    role: 'Web Developer',
    desc: 'Developing an AI-powered task management and schedule optimization web application.'
  }
]

useHead({
  link: [
    { rel: 'stylesheet', href: '/custom.css' }
  ]
})
</script>

<template>
  <div>
    <NavBar navAdminMode="" />
    <div class="page-wrapper">
      <div class="portfolio-card">
      
      <nav class="sidebar">
        <div class="sidebar-header">
          <div class="sidebar-avatar">
            <img src="/suico.jpg" alt="Gian Carlo J. Suico" />
          </div>
          <h2 class="sidebar-name">G. Suico</h2>
          <p class="sidebar-role">Developer</p>
        </div>
        
        <ul class="nav-list">
          <li v-for="link in navLinks" :key="link.id" class="nav-item">
            <button 
              @click="activeTab = link.id"
              class="nav-button"
              :class="{ 'active': activeTab === link.id }"
            >
              <svg class="nav-icon" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" :d="link.icon" />
              </svg>
              <span class="nav-text">{{ link.label }}</span>
            </button>
          </li>
        </ul>
      </nav>

      <main class="content-area">
        
        <div v-if="activeTab === 'home'" class="tab-content home-view slide-up">
          <div class="profile-picture-container">
            <img src="/suico.jpg" alt="Gian Carlo J. Suico" />
          </div>
          
          <h1 class="main-title">Gian Carlo J. Suico</h1>
          <h2 class="sub-title">Problem Solver | Web Developer | Database Engineer</h2>
          
          <p class="bio-text">
            BSCS student at Visayas State University (Expected 2028).<br/> Passionate about full-stack web development, data structures, and hardware-software integration. UISB Quiz Bowl Champion and College Honors awardee.
          </p>

          <div class="social-links">
            <a href="https://github.com/kindocarloo" target="_blank" class="social-btn" title="GitHub">
              <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" fill="currentColor" viewBox="0 0 24 24"><path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"/></svg>
            </a>
            <a href="https://www.linkedin.com/in/gian-suico-911154330/" target="_blank" class="social-btn" title="LinkedIn">
              <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" fill="currentColor" viewBox="0 0 24 24"><path d="M19 0h-14c-2.761 0-5 2.239-5 5v14c0 2.761 2.239 5 5 5h14c2.762 0 5-2.239 5-5v-14c0-2.761-2.238-5-5-5zm-11 19h-3v-11h3v11zm-1.5-12.268c-.966 0-1.75-.79-1.75-1.764s.784-1.764 1.75-1.764 1.75.79 1.75 1.764-.783 1.764-1.75 1.764zm13.5 12.268h-3v-5.604c0-3.368-4-3.113-4 0v5.604h-3v-11h3v1.765c1.396-2.586 7-2.777 7 2.476v6.759z"/></svg>
            </a>
            <a href="mailto:24-1-00321@vsu.edu.ph" class="social-btn" title="Email">
              <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" fill="currentColor" viewBox="0 0 24 24"><path d="M0 3v18h24v-18h-24zm6.623 7.929l-4.623 5.712v-9.458l4.623 3.746zm-4.141-5.929h19.035l-9.517 7.713-9.518-7.713zm5.694 7.188l3.824 3.099 3.83-3.104 5.612 6.817h-18.779l5.513-6.812zm9.208-1.264l4.616-3.741v9.348l-4.616-5.607z"/></svg>
            </a>
          </div>
        </div>

        <div v-if="activeTab === 'experience'" class="tab-content experience-view slide-up">
          <h2 class="section-title">Experience & Projects</h2>
          
          <div class="timeline-container">
            <div class="timeline-line"></div>
            <div class="timeline-grid">
              <div v-for="(item, index) in experiences" :key="index" class="timeline-item">
                <div class="timeline-dot"></div>
                <div class="timeline-content">
                  <h3 class="item-title">{{ item.title }}</h3>
                  <h4 class="item-role">{{ item.role }}</h4>
                  <p class="item-desc">{{ item.desc }}</p>
                </div>
              </div>
            </div>
          </div>
        </div>

        <div v-if="activeTab === 'contact'" class="tab-content contact-view slide-up">
          <div class="contact-icon-wrapper">
             <svg xmlns="http://www.w3.org/2000/svg" class="contact-icon" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M8 12h.01M12 12h.01M16 12h.01M21 12c0 4.418-4.03 8-9 8a9.863 9.863 0 01-4.255-.949L3 20l1.395-3.72C3.512 15.042 3 13.574 3 12c0-4.418 4.03-8 9-8s9 3.582 9 8z" />
             </svg>
          </div>
          <h2 class="section-title text-primary">Let's Connect</h2>
          <p class="contact-text">Currently a CS Sophomore at VSU, but always open to discussing new projects, tech stacks, hackathons, or hardware design.</p>
          <div class="contact-actions">
            <a href="mailto:24-1-00321@vsu.edu.ph" class="contact-btn primary-btn">Say Hello</a>
            <a href="tel:+639639623755" class="contact-btn secondary-btn">+63 963 9623755</a>
          </div>
        </div>

      </main>
    </div>
  </div>
  <Copyright />
  </div>
</template>

<style scoped>
/* CSS Variables for theming */
.page-wrapper {
  --bg-color: #E2F0EA;
  --primary: #12796A;
  --primary-hover: #0E5E53;
  --primary-light: #E7F5F2;
  --secondary: #3D9B8D;
  --text-dark: #1E293B;
  --text-gray: #64748B;
  --text-light: #94A3B8;
  --white: #ffffff;
  --sidebar-width: 280px;
  --card-shadow: 0 25px 50px -12px rgba(18, 121, 106, 0.25);
  --transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);

  min-height: 100vh;
  background: linear-gradient(135deg, var(--bg-color) 0%, #C4E4D9 100%);
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 2rem;
}

/* Global resets for the component */
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
}

.portfolio-card {
  width: 100%;
  max-width: 1100px;
  min-height: 700px;
  background-color: var(--white);
  border-radius: 1.5rem;
  box-shadow: var(--card-shadow);
  display: flex;
  flex-direction: column;
  overflow: hidden;
  position: relative;
}

/* Sidebar Navigation */
.sidebar {
  background: linear-gradient(180deg, var(--primary) 0%, var(--primary-hover) 100%);
  color: var(--white);
  padding: 3rem 2rem;
  display: flex;
  flex-direction: column;
  position: relative;
  overflow: hidden;
}

/* Abstract patterns on sidebar */
.sidebar::after {
  content: '';
  position: absolute;
  top: -50%;
  left: -50%;
  width: 200%;
  height: 200%;
  background: radial-gradient(circle, rgba(255,255,255,0.08) 0%, transparent 60%);
  z-index: 0;
  pointer-events: none;
}

.sidebar-header {
  position: relative;
  z-index: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-bottom: 3rem;
  display: none;
}

.sidebar-avatar {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  border: 3px solid rgba(255, 255, 255, 0.3);
  padding: 3px;
  margin-bottom: 1rem;
}

.sidebar-avatar img {
  width: 100%;
  height: 100%;
  border-radius: 50%;
  object-fit: cover;
}

.sidebar-name {
  font-size: 1.25rem;
  font-weight: 700;
  letter-spacing: -0.025em;
  margin-bottom: 0.25rem;
}

.sidebar-role {
  font-size: 0.85rem;
  color: #A7D8D0;
  font-weight: 500;
  text-transform: uppercase;
  letter-spacing: 0.05em;
}

.nav-list {
  position: relative;
  z-index: 1;
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
  width: 100%;
}

.nav-item {
  width: 100%;
}

.nav-button {
  width: 100%;
  background: transparent;
  border: none;
  color: rgba(255, 255, 255, 0.7);
  font-size: 1rem;
  font-weight: 500;
  cursor: pointer;
  transition: var(--transition);
  padding: 1rem 1.25rem;
  text-align: left;
  border-radius: 0.75rem;
  display: flex;
  align-items: center;
  gap: 0.75rem;
}

.nav-button:hover {
  color: var(--white);
  background: rgba(255, 255, 255, 0.1);
}

.nav-button.active {
  color: var(--primary);
  background: var(--white);
  font-weight: 600;
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
}

.nav-icon {
  width: 20px;
  height: 20px;
  flex-shrink: 0;
}

/* Main Content Area */
.content-area {
  flex: 1;
  padding: 3rem 2rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-start;
  overflow-y: auto;
  position: relative;
  background: #fdfdfd;
}

.tab-content {
  width: 100%;
  max-width: 650px;
  margin: auto;
}

.home-view {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
}

/* Profile Picture Profile View */
.profile-picture-container {
  width: 140px;
  height: 140px;
  border-radius: 50%;
  margin-bottom: 2rem;
  box-shadow: 0 10px 25px -5px rgba(18, 121, 106, 0.3);
  border: 4px solid var(--white);
  position: relative;
}

.profile-picture-container::after {
  content: '';
  position: absolute;
  inset: -8px;
  border-radius: 50%;
  border: 2px dashed var(--primary-light);
  animation: spin 15s linear infinite;
  pointer-events: none;
}

@keyframes spin {
  100% { transform: rotate(360deg); }
}

.profile-picture-container img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 50%;
  position: relative;
  z-index: 2;
}

/* Typography */
.main-title {
  color: var(--text-dark);
  font-size: 2.75rem;
  font-weight: 800;
  letter-spacing: -0.02em;
  margin-bottom: 0.75rem;
}

.sub-title {
  color: var(--secondary);
  font-size: 1.15rem;
  font-weight: 600;
  margin-bottom: 1.5rem;
  background: var(--primary-light);
  padding: 0.5rem 1.25rem;
  border-radius: 2rem;
  display: inline-block;
}

.bio-text {
  color: var(--text-gray);
  font-size: 1.05rem;
  line-height: 1.7;
  margin-bottom: 2.5rem;
  max-width: 550px;
}

.section-title {
  color: var(--text-dark);
  font-size: 2.25rem;
  font-weight: 800;
  margin-bottom: 3rem;
  letter-spacing: -0.02em;
  position: relative;
  display: inline-block;
}

.section-title.text-primary {
  color: var(--primary);
}

.section-title::after {
  content: '';
  position: absolute;
  bottom: -10px;
  left: 0;
  width: 40px;
  height: 4px;
  background-color: var(--secondary);
  border-radius: 2px;
}

.contact-view .section-title::after {
  left: 50%;
  transform: translateX(-50%);
}

/* Social Buttons */
.social-links {
  display: flex;
  gap: 1.25rem;
  justify-content: center;
}

.social-btn {
  width: 45px;
  height: 45px;
  border-radius: 12px;
  background-color: var(--white);
  color: var(--primary);
  border: 1px solid var(--primary-light);
  display: flex;
  align-items: center;
  justify-content: center;
  transition: var(--transition);
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.05);
}

.social-btn:hover {
  background-color: var(--primary);
  color: var(--white);
  transform: translateY(-3px);
  box-shadow: 0 10px 15px -3px rgba(18, 121, 106, 0.2);
}

/* Experience Timeline Grid */
.experience-view {
  padding-left: 1rem;
}

.timeline-container {
  position: relative;
}

.timeline-line {
  position: absolute;
  left: 6px;
  top: 10px;
  bottom: 0;
  width: 2px;
  background: linear-gradient(to bottom, var(--primary) 0%, var(--primary-light) 100%);
}

.timeline-grid {
  display: flex;
  flex-direction: column;
  gap: 2.5rem;
}

.timeline-item {
  position: relative;
  padding-left: 2.5rem;
}

.timeline-dot {
  position: absolute;
  left: -2px;
  top: 0.3rem;
  width: 18px;
  height: 18px;
  background-color: var(--white);
  border: 3px solid var(--primary);
  border-radius: 50%;
  box-shadow: 0 0 0 4px var(--primary-light);
  z-index: 2;
  transition: var(--transition);
}

.timeline-item:hover .timeline-dot {
  background-color: var(--primary);
  transform: scale(1.1);
}

.timeline-content {
  background: var(--white);
  border-radius: 1rem;
  padding: 1.5rem;
  border: 1px solid #f1f5f9;
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.02);
  transition: var(--transition);
}

.timeline-content:hover {
  box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.05);
  border-color: var(--primary-light);
  transform: translateX(5px);
}

.item-title {
  color: var(--text-dark);
  font-size: 1.1rem;
  font-weight: 700;
  margin-bottom: 0.25rem;
}

.item-role {
  color: var(--secondary);
  font-size: 0.85rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  margin-bottom: 0.75rem;
}

.item-desc {
  color: var(--text-gray);
  font-size: 0.95rem;
  line-height: 1.6;
}

/* Contact Tab */
.contact-view {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
}

.contact-icon-wrapper {
  width: 80px;
  height: 80px;
  background-color: var(--primary-light);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 2rem;
}

.contact-icon {
  width: 40px;
  height: 40px;
  color: var(--primary);
}

.contact-text {
  color: var(--text-gray);
  font-size: 1.1rem;
  line-height: 1.7;
  margin-bottom: 2.5rem;
  max-width: 450px;
}

.contact-actions {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  width: 100%;
  max-width: 300px;
}

.contact-btn {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 1rem 2rem;
  border-radius: 0.75rem;
  text-decoration: none;
  font-weight: 600;
  font-size: 1.05rem;
  transition: var(--transition);
}

.primary-btn {
  background-color: var(--primary);
  color: var(--white);
  box-shadow: 0 4px 6px -1px rgba(18, 121, 106, 0.2);
}

.primary-btn:hover {
  background-color: var(--primary-hover);
  transform: translateY(-2px);
  box-shadow: 0 10px 15px -3px rgba(18, 121, 106, 0.3);
}

.secondary-btn {
  background-color: var(--white);
  color: var(--text-dark);
  border: 1px solid #e2e8f0;
}

.secondary-btn:hover {
  background-color: #f8fafc;
  border-color: #cbd5e1;
}

/* Animation */
.slide-up {
  animation: slideUp 0.6s cubic-bezier(0.16, 1, 0.3, 1) forwards;
}

@keyframes slideUp {
  0% { 
    opacity: 0; 
    transform: translateY(20px); 
  }
  100% { 
    opacity: 1; 
    transform: translateY(0); 
  }
}

/* Media Queries for Desktop Layout */
@media (min-width: 768px) {
  .portfolio-card {
    flex-direction: row;
  }
  
  .sidebar {
    width: var(--sidebar-width);
    flex-shrink: 0;
  }

  .sidebar-header {
    display: flex;
  }
  
  .nav-list {
    margin-top: 0;
  }

  .content-area {
    padding: 4rem;
  }

  .timeline-grid {
    gap: 1.5rem;
  }
  
  .contact-actions {
    flex-direction: row;
    max-width: 100%;
  }
}

/* Mobile responsive adjustments */
@media (max-width: 767px) {
  .nav-list {
    flex-direction: row;
    justify-content: center;
    gap: 0.25rem;
  }
  
  .nav-item {
    width: auto;
  }
  
  .nav-button {
    padding: 0.75rem;
    border-radius: 50%;
    justify-content: center;
  }
  
  .nav-text {
    display: none;
  }
  
  .sidebar {
    padding: 1.5rem;
  }
}
</style>