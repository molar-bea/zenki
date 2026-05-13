<template>
  <client-only>
    <NavBar navAdminMode="" />
    <main id="zkMain" class="zk-main zk-policy-page">
      <section class="zk-policy-hero">
        <p class="zk-policy-kicker">Privacy Policy</p>
        <h1>Zenki Privacy Policy</h1>
        <p class="zk-policy-updated">Last updated: {{ lastUpdated }}</p>
        <p class="zk-policy-intro">
          Zenki is committed to protecting your privacy. This policy explains
          how we handle your personal data as you navigate the university
          admission process.
        </p>
      </section>

      <section class="zk-policy-card">
        <h2>1. Data Collection &amp; Purpose</h2>
        <p>
          We collect data to facilitate your admission journey. Under DPA 2012
          and GDPR, we process data based on Consent and Contractual Necessity.
        </p>
        <div class="zk-policy-grid">
          <article>
            <h3>Identity &amp; Contact</h3>
            <p>
              Name, email, and phone number are used to send status updates and
              appointment reminders.
            </p>
          </article>
          <article>
            <h3>Academic Profile</h3>
            <p>
              GPA and test scores are used to perform the Eligibility Check.
            </p>
          </article>
          <article>
            <h3>Document Metadata</h3>
            <p>
              We track the status of your physical documents, such as “Birth
              Certificate Prepared”.
            </p>
          </article>
          <article>
            <h3>Digital Pre-checks</h3>
            <p>
              If you upload photos of documents for preliminary review, these
              are treated as Sensitive Personal Information.
            </p>
          </article>
        </div>
      </section>

      <section class="zk-policy-card">
        <h2>2. Physical Document Handling</h2>
        <p>The app acts as a tracking interface only.</p>
        <ul>
          <li>
            The University Registrar remains the sole custodian of your physical
            copies.
          </li>
          <li>
            App administrators only see the status of your physical submission,
            such as “Received at Window 2”, to update your digital dashboard.
          </li>
        </ul>
      </section>

      <section class="zk-policy-card">
        <h2>3. Your Rights as a Data Subject</h2>
        <p>Regardless of your location, we grant you the following rights:</p>
        <ul>
          <li>
            <strong>Right to Information:</strong> To know if your data is being
            processed.
          </li>
          <li>
            <strong>Right to Access &amp; Rectification:</strong> To view and
            correct your profile and academic data.
          </li>
          <li>
            <strong>Right to Erasure (Right to be Forgotten):</strong> To request
            deletion of your account if you withdraw your application.
          </li>
          <li>
            <strong>Right to Data Portability:</strong> To receive a digital copy
            of your application history.
          </li>
        </ul>
      </section>

      <section class="zk-policy-card">
        <h2>4. Data Storage &amp; Security</h2>
        <ul>
          <li>
            <strong>Security:</strong> We use industry-standard encryption
            (SSL/TLS) for data in transit and at rest.
          </li>
          <li>
            <strong>Retention:</strong> Data is kept only for the duration of
            the admission cycle. If you are admitted, your data migrates to the
            Student Information System. If not, data is purged after one (1)
            year unless otherwise required by law.
          </li>
        </ul>
      </section>

      <section class="zk-policy-card">
        <h2>5. Third-Party Sharing</h2>
        <p>We do not sell your personal data. Data is only shared with:</p>
        <ul>
          <li>
            <strong>University Departments:</strong> Registrar, Admissions
            Committee, and Accounting for processing your enrollment.
          </li>
          <li>
            <strong>Technical Partners:</strong> Cloud hosting providers who are
            strictly bound by Data Processing Agreements (DPA).
          </li>
        </ul>
      </section>

      <section class="zk-policy-card">
        <h2>6. International Transfers (GDPR)</h2>
        <p>
          If you are accessing this app from the EU, your data is transferred to
          our servers in the Philippines. We ensure “Adequate Protection”
          through Standard Contractual Clauses.
        </p>
      </section>
    </main>
    <AboutUs />
    <Copyright />
  </client-only>
</template>

<script setup lang="ts">
import { useSeoMeta, useHead } from "@vueuse/head";

const title = "Zenki | Privacy Policy";
const description =
  "Learn about how Zenki handles your data and privacy during the admission process.";

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

const lastUpdated = "March 12, 2026";
</script>

<style scoped>
.zk-policy-page {
  width: min(1080px, calc(100% - 32px));
  margin: 0 auto;
  padding: 88px 0 32px;
}

.zk-policy-hero,
.zk-policy-card {
  background: rgba(255, 255, 255, 0.86);
  border: 1px solid rgba(0, 0, 0, 0.08);
  border-radius: 20px;
  box-shadow: 0 18px 40px rgba(54, 67, 56, 0.08);
  backdrop-filter: blur(6px);
}

.zk-policy-hero {
  padding: 32px;
  margin-bottom: 20px;
}

.zk-policy-kicker {
  margin: 0 0 8px;
  text-transform: uppercase;
  letter-spacing: 0.14em;
  font-size: 0.75rem;
  font-weight: 700;
  color: #3f7d58;
}

.zk-policy-hero h1 {
  margin: 0;
  font-family: "DM Serif Display", Georgia, serif;
  font-size: clamp(2.2rem, 4vw, 3.8rem);
  line-height: 1;
  color: #243428;
}

.zk-policy-updated {
  margin: 12px 0 0;
  font-size: 0.95rem;
  color: #6d6d6d;
}

.zk-policy-intro {
  margin: 18px 0 0;
  max-width: 68ch;
  font-size: 1.05rem;
  line-height: 1.75;
  color: #37413b;
}

.zk-policy-card {
  padding: 28px 32px;
  margin-top: 16px;
}

.zk-policy-card h2 {
  margin: 0 0 12px;
  font-size: 1.4rem;
  line-height: 1.25;
  color: #243428;
}

.zk-policy-card h3 {
  margin: 0 0 8px;
  font-size: 1rem;
  color: #2f3c33;
}

.zk-policy-card p,
.zk-policy-card li {
  color: #39453d;
  line-height: 1.75;
}

.zk-policy-card p {
  margin: 0;
}

.zk-policy-card ul {
  margin: 14px 0 0;
  padding-left: 20px;
}

.zk-policy-card li + li {
  margin-top: 8px;
}

.zk-policy-grid {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 16px;
  margin-top: 18px;
}

.zk-policy-grid article {
  padding: 18px;
  border-radius: 16px;
  background: linear-gradient(180deg, rgba(63, 125, 88, 0.07), rgba(161, 136, 127, 0.04));
  border: 1px solid rgba(63, 125, 88, 0.12);
}

@media (max-width: 720px) {
  .zk-policy-page {
    width: min(100% - 20px, 1080px);
    padding-top: 74px;
  }

  .zk-policy-hero,
  .zk-policy-card {
    padding-left: 20px;
    padding-right: 20px;
  }

  .zk-policy-grid {
    grid-template-columns: 1fr;
  }
}
</style>

<style></style>
