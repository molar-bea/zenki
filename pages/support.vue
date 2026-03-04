<script setup lang="ts">

import { useSeoMeta, useHead } from '@vueuse/head';

const title = "Zenki | Home";
const description = "An application to systematize admission process.";

useSeoMeta({
 title: () => title,
 description: () => description,
 charset: "utf-8",
 viewport: "width=device-width, initial-scale=1.0"
});

useHead({
 link: [
 {rel: 'icon', type: 'image/png', href: '/logo.png'},
 {rel: 'stylesheet', href: '/reset.css'}
 ]
});
</script>

<template>
    <client-only>
        <NavBar />
        <Support />
        <Copyright />
    </client-only>
</template>
