<script setup lang="ts"></script>

<template>
    <client-only>
        <NavBar />
        <div id="zkMain" class="zk-main"></div>
        <Copyright />
    </client-only>
</template>

<script setup lang="ts">
import { useSeoMeta, useHead } from '@vueuse/head';

const title = "Zenki | Privacy Policy";
const description = "Learn about how Zenki handles your data and privacy during the admission process.";

useSeoMeta({
 title: () => title,
 description: () => description,
 charset: "utf-8",
 viewport: "width=device-width, initial-scale=1.0"
});

useHead({
 link: [
 {rel: 'icon', type: 'image/png', href: '/logo.png'},
 {rel: 'stylesheet', href: '/reset.css'},
 {rel: 'stylesheet', href: '/custom.css'} ,
 {rel: 'preconnect', href: 'https://fonts.googleapis.com'},
 {rel: 'preconnect', href: 'https://fonts.gstatic.com', crossorigin: ''},
 {rel: 'stylesheet', href: 'https://fonts.googleapis.com/css2?family=DM+Serif+Display:ital@0;1&family=IBM+Plex+Sans:ital,wght@0,100..700;1,100..700&display=swap" rel="stylesheet'},
 ]
});
</script>

<style scoped></style>
<style></style>

