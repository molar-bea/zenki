 <script setup lang="ts"></script>
<template>
    <client-only>
        <NavBar />
        <div id="zkMain" class="zk-main"></div>
        <Cookies />
        <Copyright />
    </client-only>
</template>


<script setup lang="ts">
    import { useSeoMeta, useHead } from '@vueuse/head';
    const title = "Zenki | Home";
    const description = "An application that guides students with the admission process in the university.";
    const globalDelay = 500;
    const allowCookies = useCookie<boolean>("allowCookies", {
        sameSite: "none",
        secure: true,
        maxAge: 60 * 60 * 24, 
    });

    //allowCookies.value =false;
    allowCookies.value = allowCookies.value || false;
    async function loadModal() {

        const cookieModal = document.getElementById("zkCookieModal") as HTMLDivElement;
        const cookieBox = document.getElementById("zkCookieBox") as HTMLDivElement;
        const cookieX = document.getElementById("zkCookieX") as HTMLDivElement;
        const cookieOK = document.getElementById("zkCookieOK") as HTMLDivElement;
        if ( !cookieModal || !cookieBox || !cookieX || !cookieOK ) return;
        if (allowCookies.value === true) {
            allowAllCookies();
            return;
        }

        showCookiePopup();

        cookieX.addEventListener("click", (e) => {
            showCookiePopup(false);
        });

        cookieOK.addEventListener("click", (e) => {
            allowAllCookies();
        });

    }

    async function showCookiePopup(show: boolean = true) {

        const cookieBox = document.getElementById("zkCookieBox") as HTMLDivElement;
        const cookieModal = document.getElementById("zkCookieModal") as HTMLDivElement;
        if (!cookieBox || !cookieModal) {
            setTimeout(showCookiePopup, 50);
            return;
        }

        if (!show) {
            cookieBox.classList.add("zk-hidden");
            cookieModal.classList.add("zk-hidden");
            return;
        }

        cookieBox.classList.remove("zk-hidden");
        cookieModal.classList.remove("zk-hidden");

    }

    let lastCookieClicked = 0;

    async function allowAllCookies() {
        if (lastCookieClicked >= Date.now() - globalDelay) return;
        lastCookieClicked = Date.now();
        allowCookies.value = true;
        showCookiePopup(false);

    }

    onMounted(() => {
        setTimeout(() => {
        loadModal();
        }, 1);
    });


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