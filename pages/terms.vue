<script lang="ts"></script>

<template>
  <client-only>
    <NavBar navAdminMode="" />
    <div id="zkMain" class="zk-main">
      <div class="terms-wrapper">
        <header class="terms-header">
          <h1>Terms of Service</h1>
        </header>

        <div class="terms-content">
          <section>
            <h2>1. Scope of Service</h2>
            <p>
              The App is a guidance tool for university admissions. 
              <strong>Important:</strong> The App facilitates the organization and tracking of applications; 
              however, official admission is contingent upon the successful submission and verification 
              of physical documents at the University Registrar.
            </p>
          </section>

          <section>
            <h2>2. Data Collection (DPA & GDPR Compliance)</h2>
            <p>To provide our services, we collect the following Personal Data:</p>
            <ul>
              <li><strong>Identity Data:</strong> Name, date of birth, and student identification numbers.</li>
              <li><strong>Contact Data:</strong> Email address and phone number for status notifications.</li>
              <li><strong>Academic Data:</strong> GPA, test scores, and previous school information for eligibility checks.</li>
              <li><strong>Digital Pre-checks:</strong> Images of documents uploaded for preliminary review.</li>
            </ul>
          </section>

          <section>
            <h2>3. Purpose of Processing</h2>
            <p>Your data is processed based on Contractual Necessity and Legitimate Interest:</p>
            <ul>
              <li>To verify eligibility for specific academic programs.</li>
              <li>To manage appointment scheduling for physical document drop-offs.</li>
              <li>To provide real-time updates on your admission status.</li>
            </ul>
          </section>

          <section>
            <h2>4. Data Subject Rights</h2>
            <p>Under the Data Privacy Act of 2012 (PH) and GDPR (EU), you have the right to:</p>
            <ul>
              <li><strong>Access & Rectification:</strong> Request a copy of your data or correct inaccuracies.</li>
              <li><strong>Erasure (Right to be Forgotten):</strong> Request deletion of your account (subject to university record-keeping laws).</li>
              <li><strong>Data Portability:</strong> Request a digital copy of your provided data.</li>
              <li><strong>Withdraw Consent:</strong> Withdraw your consent for data processing at any time.</li>
            </ul>
          </section>

          <section>
            <h2>5. Data Retention & Security</h2>
            <p>
              <strong>Storage:</strong> Digital copies uploaded for "pre-checks" are stored on secured servers with AES-256 encryption.
            </p>
            <p>
              <strong>Retention:</strong> If an application is unsuccessful or withdrawn, personal data is purged after 1 year, unless a longer period is required by the Education Act.
            </p>
            <p>
              <strong>Physical Documents:</strong> The App does not "store" physical documents; once handed to the university, those are governed by the University’s Manual of Regulations.
            </p>
          </section>

          <section>
            <h2>6. Third-Party Sharing</h2>
            <p>We do not sell your data. Data is only shared with:</p>
            <ul>
              <li>Internal University Departments (Registrar, Dean’s Office, Accounting).</li>
              <li>Cloud service providers (as data processors) under strict confidentiality agreements.</li>
            </ul>
          </section>

          <section>
            <h2>7. User Responsibilities</h2>
            <ul>
              <li>Users must provide truthful and accurate information.</li>
              <li>Users acknowledge that the digital "pre-check" does not constitute final acceptance of a document; the physical copy remains the "Source of Truth."</li>
            </ul>
          </section>

          <div class="acceptance-box">
            <h3>Acceptance</h3>
            <p>
              By clicking "I Agree" or using the App, you signify your "Informed Consent" as defined by the DPA of 2012 and "Explicit Consent" under the GDPR.
            </p>
          </div>
        </div>
      </div>
    </div>
    <Copyright />
  </client-only>
</template>

<script setup lang="ts">
import { useSeoMeta, useHead } from "@vueuse/head";

const title = "Zenki | Terms of Service";
const description = "Terms of Service and Privacy Policy for Zenki University Admission Guide.";

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
  padding: 80px 20px;
  background-color: #ffffff;
  color: #1a1a1a;
  min-height: 100vh;
  display: flex;
  justify-content: center;
}

.terms-wrapper {
  max-width: 750px;
  width: 100%;
}

.terms-header {
  margin-bottom: 3rem;
  border-bottom: 1px solid #eaeaea;
  padding-bottom: 1.5rem;
}

h1 {
  font-family: 'DM Serif Display', serif;
  font-size: clamp(2.5rem, 5vw, 3.5rem);
  line-height: 1.1;
  margin-bottom: 0.5rem;
}

.subtitle {
  font-family: 'IBM Plex Sans', sans-serif;
  color: #666;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-size: 0.85rem;
}

.terms-content {
  font-family: 'IBM Plex Sans', sans-serif;
  line-height: 1.7;
}

h2 {
  font-family: 'DM Serif Display', serif;
  font-size: 1.75rem;
  margin: 2.5rem 0 1rem 0;
  color: #222;
}

p {
  margin-bottom: 1.2rem;
}

ul {
  margin-bottom: 1.5rem;
  padding-left: 1.2rem;
}

li {
  margin-bottom: 0.6rem;
}

strong {
  font-weight: 600;
}

.acceptance-box {
  margin-top: 4rem;
  padding: 2rem;
  background-color: #f9f9f9;
  border-radius: 8px;
  border-left: 4px solid #1a1a1a;
}

.acceptance-box h3 {
  font-family: 'DM Serif Display', serif;
  font-size: 1.5rem;
  margin-bottom: 1rem;
}

.acceptance-box p {
  margin-bottom: 0;
  font-style: italic;
}

@media (max-width: 600px) {
  .zk-main {
    padding: 40px 15px;
  }
}
</style>