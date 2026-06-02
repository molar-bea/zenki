<script setup lang="ts">
import { ref, onMounted } from "vue";

const fullName = "Ervin James Caballes";
const title = `${fullName} | Personal Page`;
const description = "Resume-style personal page of Ervin James Caballes.";
const profilePhoto = "/ecaballes-photo.jpg";
const fallbackPhoto = "/CABALLES.jpg";
const currentPhoto = ref(profilePhoto);

function onPhotoError() {
  currentPhoto.value = fallbackPhoto;
}

onMounted(() => {
  document.title = title;

  let metaDescription = document.querySelector('meta[name="description"]');
  if (metaDescription) {
    metaDescription.setAttribute('content', description);
  } else {
    const meta = document.createElement('meta');
    meta.name = 'description';
    meta.content = description;
    document.head.appendChild(meta);
  }

  let viewport = document.querySelector('meta[name="viewport"]');
  if (!viewport) {
    const meta = document.createElement('meta');
    meta.name = 'viewport';
    meta.content = 'width=device-width, initial-scale=1.0';
    document.head.appendChild(meta);
  }
});

onMounted(() => {
  if (!document.querySelector('link[href="/reset.css"]')) {
    const resetLink = document.createElement('link');
    resetLink.rel = 'stylesheet';
    resetLink.href = '/reset.css';
    document.head.appendChild(resetLink);
  }

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
    <nav class="nav-bar" v-if="false"></nav>

    <main class="em-wrap">
      <section class="em-hero">
        <img
          class="em-avatar"
          :src="currentPhoto"
          @error="onPhotoError"
          alt="Ervin James Caballes professional profile"
        />

        <div class="em-intro">
          <p class="em-kicker">Personal Page</p>
          <h1 class="em-name">Ervin James Caballes</h1>
          <p class="em-contact">Leyte, Philippines | +63 963 355 0908 | caballeservinjames889@gmail.com  </p>
          <p class="em-summary">
            Aiming to be a software engineer with experience in full-stack development
            and database optimization while focusing on delivering high-performance
            code and intuitive user experiences.
          </p>
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
          <h2>Projects</h2>

          <h3>Library Management System (2024)</h3>
          <ul>
            <li>Built a full-stack web application managing 300+ book titles, automating late-fee calculations to reduce administrative work by 20+ minutes per day.</li>
            <li>Engineered optimized SQL queries with indexing and joins, reducing API response time by 60% for catalog searches and filtering.</li>
            <li>Designed a responsive user interface with real-time form validation, preventing invalid ISBN entries and reducing data input errors by 40%.</li>
          </ul>

          <h3>Mathematics-Based Game Website (2024)</h3>
          <ul>
            <li>Designed a full-stack interactive platform featuring logic-based math games to boost engagement for students struggling with math logic.</li>
            <li>Developed a custom game engine with dynamic difficulty scaling, automating the generation of logic puzzles to adapt to individual student skill levels.</li>
          </ul>

          <h3>Collaborative Web Application (2023)</h3>
          <ul>
            <li>Pioneered interactive features within the StudyWithMe application, empowering peer-to-peer learning and collaborative brainstorming sessions, leading to 25% less system bugs/crashes.</li>
            <li>Engineered features for group study and brainstorming, facilitating peer support in a synchronized, interactive online environment.</li>
            <li>Architected real-time room logic to support seamless multi-user collaboration and interactive session management.</li>
          </ul>
        </article>

        <article class="em-card em-card-wide">
          <h2>Skills</h2>
          <p><strong>Programming Languages:</strong> C/C++, Java, Python</p>
          <p><strong>Web Technologies:</strong> HTML, CSS, JavaScript</p>
          <p><strong>Database:</strong> MariaDB, MySQL</p>
          <p><strong>DevOps:</strong> GitHub</p>
        </article>
      </section>
    </main>

    <div class="copyright">
      <p>&copy; {{ new Date().getFullYear() }} Ervin James Caballes</p>
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