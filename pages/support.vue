<script setup lang="ts">
import NavBar from "@/components/NavBar.vue";
import Copyright from "@/components/Copyright.vue";
import { useSeoMeta, useHead } from "@vueuse/head";

// Generate today's date in a readable format
const today = new Date();
const formattedDate = today.toLocaleDateString("en-US", {
  year: "numeric",
  month: "long",
  day: "numeric",
});

const title = "Zenki | Support";
const description =
  "Get help and support with using Zenki for the university admission process.";

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
    {
      rel: "stylesheet",
      href: "https://fonts.googleapis.com/css2?family=DM+Serif+Display:ital@0;1&family=IBM+Plex+Sans:ital,wght@0,100..700;1,100..700&display=swap",
    },
  ],
});
</script>

<template>
  <client-only>
    <!-- Navigation -->
    <NavBar navAdminMode="" />

    <!-- Main Content -->
    <main id="zkMain" class="zk-main support-page">
      <h1>Account Deletion</h1>
      <p class="effective-date">
        <strong>Effective Date:</strong> {{ formattedDate }}
      </p>

      <section>
        <h2>Data Retention and Deletion</h2>
        <p>
          You can request the deletion of your account and all associated data at any time.
          When you delete your account, all your personal data and inputted information will
          be permanently removed from our systems.
        </p>
        <p>
          Please note that account deletion is irreversible. Once your account is deleted, you
          will lose access to all your data and any features associated with your account.    
      </p>
      </section>

      <!-- Compact Contact Support Section -->
      <section class="support-contact">
        <h2>Contact Support</h2>
        <ul>
          <li>Email: <a href="mailto:zenki.support@gmail.com">zenki.support@gmail.com</a></li>
          <li>Help Center: <a href="/help">Zenki Help Center</a></li>
        </ul>
      </section>
    </main>

    <!-- Footer -->
    <AboutUs />
    <Copyright />
  </client-only>
</template>

<style scoped>
.support-page {
  max-width: 800px;
  margin: 80px auto 40px; /* space below navbar */
  padding: 2rem;
  background-color: #fff;
  border-radius: 10px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
  color: #333;
  line-height: 1.6;
}

.support-page h1 {
  font-family: "DM Serif Display", serif;
  font-size: 2rem;
  margin-bottom: 1rem;
  color: #2e4a23;
}

.support-page h2 {
  font-size: 1.4rem;
  margin-top: 1.5rem;
  margin-bottom: 0.8rem;
  color: #3f7d58;
}

.support-page p {
  margin-bottom: 1rem;
}

.effective-date {
  background: #f2f4f7;
  padding: 0.8rem;
  border-left: 4px solid #81c784;
  border-radius: 6px;
}

/* Compact Contact Support Section */
.support-contact {
  margin-top: 1.5rem;
  padding: 1rem 1.2rem;
  background-color: #f2f4f7;
  border-radius: 6px;
  border: 1px solid #e0e0e0;
}

.support-contact h2 {
  font-size: 1.2rem;
  margin-bottom: 0.6rem;
  color: #3f7d58;
  font-family: "DM Serif Display", serif;
}

.support-contact ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

.support-contact ul li {
  margin-bottom: 0.4rem;
  color: #444;
}

.support-contact a {
  color: #3f7d58;
  font-weight: 500;
  text-decoration: none;
}

.support-contact a:hover {
  text-decoration: underline;
}
</style>
