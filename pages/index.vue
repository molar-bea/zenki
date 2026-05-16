<template>
<client-only>
<NavBar :navAdminMode="navAdminMode" />
<div id="zkMain" class="zk-main"></div>
<Cookies />
<Copyright />
</client-only>
</template>
<script setup lang="ts">
const title = "Zenki";
const description = "An application that guides students with the admission process in the university.";
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
const globalDelay = 500;
const cookieOptions = {
sameSite: "none" as const,
secure: true,
maxAge: 60 * 60 * 24,
};
const allowCookies = useCookie<boolean>("allowCookies", cookieOptions);
allowCookies.value = allowCookies.value ?? false;
const emailAddress = useCookie<string>("emailAddress", cookieOptions);
emailAddress.value = emailAddress.value ?? "";
const accessToken = useCookie<string>("accessToken", cookieOptions);
accessToken.value = accessToken.value ?? "";
const userLevel = useCookie<number>("userLevel", cookieOptions);
userLevel.value = userLevel.value ?? -1;
const fullName = useCookie<string>("fullName", cookieOptions);
fullName.value = fullName.value ?? "";
const router = useRouter();
const navAdminMode = computed(() =>
userLevel.value >= 2 ? "zk-nav-admin" : "",
);
function getByID<T extends HTMLElement>(id: string) {
return document.getElementById(id) as T;
}
function checkAuthorizations() {
if (userLevel.value === -1) {
if (router.currentRoute.value.path !== "/") {
router.push("/");
}
return;
} else if (userLevel.value >= 2) {
router.push("/admin");
}

const navGuest = getByID<HTMLDivElement>("zkNavGuest");
const navBasic = getByID<HTMLDivElement>("zkNavBasic");
const navAdmin = getByID<HTMLDivElement>("zkNavAdmin");
const navLogout = getByID<HTMLDivElement>("zkNavBasicLogout");
const pageTitle = getByID<HTMLSpanElement>("zkPageTitle");
if (!navGuest || !navBasic || !navAdmin || !navLogout || !pageTitle) return;
navLogout.addEventListener("click", () => {
emailAddress.value = "";
accessToken.value = "";
userLevel.value = -1;
fullName.value = "";
router.push("/signin");
});
navGuest.remove();
navAdmin.remove();
navBasic.classList.remove("zk-hidden");
pageTitle.classList.remove("zk-hidden");
loadModal();
}
function loadModal() {
const cookieModal = getByID<HTMLDivElement>("zkCookieModal");
const cookieX = getByID<HTMLDivElement>("zkCookieX");
const cookieOK = getByID<HTMLDivElement>("zkCookieOK");
if (!cookieModal || !cookieX || !cookieOK) return;
if (allowCookies.value) {
allowAllCookies();
return;
}
showCookiePopup();
cookieX.addEventListener("click", () => {
showCookiePopup(false);
});
cookieOK.addEventListener("click", () => {
allowAllCookies();
});
}
function showCookiePopup(show: boolean = true) {
const cookieBox = getByID<HTMLDivElement>("zkCookieBox");
const cookieModal = getByID<HTMLDivElement>("zkCookieModal");
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
function allowAllCookies() {
if (lastCookieClicked >= Date.now() - globalDelay) return;
lastCookieClicked = Date.now();
allowCookies.value = true;
showCookiePopup(false);
}
onMounted(async () => {
await nextTick();
checkAuthorizations();
});
</script>