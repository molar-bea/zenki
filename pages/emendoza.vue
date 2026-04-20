<script setup lang="ts">
import { ref } from "vue";
import { useSeoMeta, useHead } from "@vueuse/head";

const fullName = "Exzon Y. Mendoza II";
const title = `${fullName} | Personal Page`;
const description = "Resume-style personal page of Exzon Y. Mendoza II.";
const profilePhoto = "/emendoza-photo.jpg";
const fallbackPhoto = "/MENDOZA.jpg";
const currentPhoto = ref(profilePhoto);

function onPhotoError() {
  currentPhoto.value = fallbackPhoto;
}

// Set document title and meta tags dynamically
onMounted(() => {
  document.title = title;
  
  // Update meta description
  let metaDescription = document.querySelector('meta[name="description"]');
  if (metaDescription) {
    metaDescription.setAttribute('content', description);
  } else {
    const meta = document.createElement('meta');
    meta.name = 'description';
    meta.content = description;
    document.head.appendChild(meta);
  }
  
  // Add viewport meta if not exists
  let viewport = document.querySelector('meta[name="viewport"]');
  if (!viewport) {
    const meta = document.createElement('meta');
    meta.name = 'viewport';
    meta.content = 'width=device-width, initial-scale=1.0';
    document.head.appendChild(meta);
  }
});

// Add stylesheets on mount
onMounted(() => {
  // Check if reset.css is already added
  if (!document.querySelector('link[href="/reset.css"]')) {
    const resetLink = document.createElement('link');
    resetLink.rel = 'stylesheet';
    resetLink.href = '/reset.css';
    document.head.appendChild(resetLink);
  }
  
  // Check if custom.css is already added
  if (!document.querySelector('link[href="/custom.css"]')) {
    const customLink = document.createElement('link');
    customLink.rel = 'stylesheet';
    customLink.href = '/custom.css';
    document.head.appendChild(customLink);
  }
});
</script>

<template>
  <div>
    <!-- Remove client-only wrapper or replace with div -->
    <!-- If NavBar and Copyright components exist, import them -->
    <nav class="nav-bar" v-if="false">
      <!-- Temporary placeholder for NavBar -->
    </nav>

    <main class="em-wrap">
      <section class="em-hero">
        <img
          class="em-avatar"
          :src="currentPhoto"
          @error="onPhotoError"
          alt="Exzon Y. Mendoza II professional profile"
        />

        <div class="em-intro">
          <p class="em-kicker">Personal Page</p>
          <h1 class="em-name">Exzon Y. Mendoza II</h1>
          <p class="em-contact">Leyte, PH | +63 927 197 0911 | lellugetdk@gmail.com</p>
          <p class="em-contact">
            <a href="https://github.com/Floranboi" target="_blank" rel="noopener noreferrer">
              github.com/Floranboi
            </a>
          </p>
          <p class="em-summary">Aspiring Full-Stack Developer/Game Developer</p>
        </div>
      </section>

      <section class="em-grid">
        <article class="em-card em-card-wide">
          <h2>Education</h2>
          <h3>Visayas State University</h3>
          <p class="em-muted">Bachelor of Science in Computer Science</p>
          <p class="em-muted">2024 - Present</p>
          <ul>
            <li>Ongoing bachelor&apos;s degree (2nd Year).</li>
          </ul>
        </article>

        <article class="em-card em-card-wide">
          <h2>Experience</h2>
          <h3>Front End Website</h3>
          <p class="em-muted">Dec 2025 - Present</p>
          <ul>
            <li>Developed 1 responsive, mobile-first web interfaces using Figma and modern CSS frameworks.</li>
            <li>Optimized asset loading handling over 200 lines of code.</li>
            <li>General UX graphic designing with custom and free-use image/art materials.</li>
            <li>Refactored legacy code to adhere to web standards, ensuring WCAG 2.1 compliance.</li>
          </ul>

          <h3>Back End Server-Side Logic and Database</h3>
          <p class="em-muted">Aug 2024 - Jun 2025</p>
          <ul>
            <li>Designed normalized SQL schemas and indexed tables to improve data retrieval.</li>
            <li>Implemented data handling for 50+ mock users during testing.</li>
            <li>Provided CLI front-end tooling for database updates through phpMyAdmin.</li>
          </ul>

          <h3>Server Hosting (Video Games)</h3>
          <p class="em-muted">Dec 2025 - Jan 2026</p>
          <ul>
            <li>Managed 100+ mod dependencies and resolved conflicts to avoid runtime crashes.</li>
            <li>Maintained a Windows-based Minecraft server with 99% uptime for active players.</li>
          </ul>
        </article>

        <article class="em-card">
          <h2>Skills</h2>
          <p><strong>Programming Languages:</strong> Java, C/C++, Python, JavaScript</p>
          <p><strong>Web Technologies:</strong> HTML, CSS, Figma</p>
          <p><strong>Database and Server:</strong> SQL(MySQL), phpMyAdmin, Database Design, Linux/Windows Server Administration</p>
          <p><strong>Tools and Version Control:</strong> Git, GitHub, GitKraken, VSCode, Photoshop</p>
        </article>

        <article class="em-card">
          <h2>Projects</h2>
          <ul>
            <li><strong>itch.io Game Jam Entry:</strong> Volunteered and coordinated in a 2-man team developing a 2D rhythmic button-masher game within 1 week using Godot.</li>
            <li><strong>Student Database SQL:</strong> Built a CRUD app with phpMyAdmin, executed 50+ test operations, and implemented 15+ SQL triggers and stored procedures for validation and reporting.</li>
          </ul>
        </article>
      </section>
    </main>

    <div class="copyright">
      <!-- Temporary placeholder for Copyright component -->
      <p>&copy; {{ new Date().getFullYear() }} Exzon Y. Mendoza II</p>
    </div>
  </div>
</template>

<style scoped>
.em-wrap {
  min-height: calc(100vh - 120px);
  padding: 40px 20px 60px;
  background:
    radial-gradient(circle at 20% 15%, #f6e5d6 0%, transparent 40%),
    radial-gradient(circle at 80% 10%, #dceaf6 0%, transparent 35%),
    linear-gradient(135deg, #fcfaf6 0%, #f2f5f8 100%);
}

.em-hero {
  max-width: 980px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: 140px 1fr;
  gap: 24px;
  align-items: center;
  background: rgba(255, 255, 255, 0.82);
  border: 1px solid #d2d9e0;
  border-radius: 18px;
  padding: 24px;
  box-shadow: 0 12px 24px rgba(24, 34, 45, 0.08);
}

.em-name {
  font-size: clamp(1.9rem, 3vw, 2.8rem);
  line-height: 1.1;
  margin: 8px 0;
}

.em-avatar {
  width: 132px;
  height: 132px;
  border-radius: 50%;
  border: 3px solid #223347;
  background: #fff;
  object-fit: cover;
  object-position: center 20%;
  display: block;
  flex-shrink: 0;
}

.em-intro {
  font-family: "Space Grotesk", sans-serif;
  color: #1a2a3a;
}

.em-kicker {
  font-size: 0.9rem;
  text-transform: uppercase;
  letter-spacing: 0.12em;
  color: #4a6075;
  margin: 0;
}

.em-contact {
  margin: 4px 0;
  color: #2b455f;
  font-weight: 500;
}

.em-contact a {
  color: #2b455f;
  text-decoration: none;
  border-bottom: 1px solid transparent;
  transition: border-color 0.2s;
}

.em-contact a:hover {
  border-bottom-color: #2b455f;
}

.em-summary {
  margin-top: 10px;
  max-width: 72ch;
  line-height: 1.6;
}

.em-grid {
  max-width: 980px;
  margin: 22px auto 0;
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 16px;
}

.em-card {
  background: rgba(255, 255, 255, 0.84);
  border: 1px solid #d2d9e0;
  border-radius: 14px;
  padding: 18px 18px 16px;
  box-shadow: 0 10px 20px rgba(24, 34, 45, 0.06);
  color: #1a2a3a;
  font-family: "Source Serif 4", serif;
}

.em-card-wide {
  grid-column: 1 / -1;
}

.em-card h2 {
  margin: 0 0 10px;
  font-family: "Space Grotesk", sans-serif;
  font-size: 1.05rem;
  color: #1e3550;
}

.em-card h3 {
  margin: 12px 0 4px;
  font-size: 1.08rem;
}

.em-card p {
  margin: 4px 0;
  line-height: 1.55;
}

.em-muted {
  color: #4c6074;
}

.em-card ul {
  margin: 6px 0 0;
  padding-left: 18px;
}

.em-card li {
  margin: 4px 0;
  line-height: 1.45;
}

.copyright {
  text-align: center;
  padding: 20px;
  font-size: 0.85rem;
  color: #6b7c8f;
  background: rgba(255, 255, 255, 0.6);
  border-top: 1px solid #d2d9e0;
}

@media (max-width: 760px) {
  .em-hero {
    grid-template-columns: 1fr;
    text-align: center;
    justify-items: center;
  }

  .em-summary {
    max-width: 100%;
  }

  .em-grid {
    grid-template-columns: 1fr;
  }

  .em-card-wide {
    grid-column: auto;
  }
}
</style>