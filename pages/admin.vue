<script lang="ts"></script>

<template>
  <client-only>
    <NavBar :navAdminMode="navAdminMode" />
    <div id="zkMain" class="zk-main">
      <span id="zkSimpleHello" class="zk-simple-hello zk-hidden">
        Hello, {{ fullName }}!
      </span>
    </div>
    <Cookies />
    <AboutUs />
    <Copyright />
  </client-only>
</template>

<script setup lang="ts">
import { useSeoMeta, useHead } from "@vueuse/head";
import { useRouter } from "vue-router";

const title = "Zenki | Home";
const description =
  "An application that guides students with the admission process in the university.";

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

/* Cookies */
const globalDelay = 500;

const allowCookies = useCookie<boolean>("allowCookies", {
  sameSite: "none",
  secure: true,
  maxAge: 60 * 60 * 24,
});
allowCookies.value = allowCookies.value ?? false;

const retries = useCookie<number>("retries", {
  sameSite: "none",
  secure: true,
  maxAge: 60 * 60,
});
retries.value = retries.value ?? 0;

const username = useCookie<string>("username", {
  sameSite: "none",
  secure: true,
  maxAge: 60 * 60 * 24,
});
username.value = username.value ?? "";

const accessToken = useCookie<string>("accessToken", {
  sameSite: "none",
  secure: true,
  maxAge: 60 * 60 * 24,
});
accessToken.value = accessToken.value ?? "";

const userLevel = useCookie<number>("userLevel", {
  sameSite: "none",
  secure: true,
  maxAge: 60 * 60 * 24,
});
userLevel.value = userLevel.value ?? -1;

const fullName = useCookie<string>("fullName", {
  sameSite: "none",
  secure: true,
  maxAge: 60 * 60 * 24,
});
fullName.value = fullName.value ?? "";

/* Access Control */
const router = useRouter();
let navAdminMode = userLevel.value >= 2 ? "zk-nav-admin" : "";

function getByID<T extends HTMLElement>(id: string) {
  return document.getElementById(id) as T;
}
function checkAuthorizations() {
  if (!accessToken.value) {
    router.push("/login");
  } else if (userLevel.value < 2) {
    router.push("/");
  }

  const navBasic = getByID<HTMLDivElement>("zkNavBasic");
  const navAdmin = getByID<HTMLDivElement>("zkNavAdmin");
  const navLogout = getByID<HTMLDivElement>("zkNavAdminLogout");
  const simpleHello = getByID<HTMLSpanElement>("zkSimpleHello");

  if (!navBasic || !navAdmin || !navLogout || !simpleHello) return;

  navLogout.addEventListener("click", () => {
    retries.value = 0;
    username.value = "";
    accessToken.value = "";
    userLevel.value = -1;
    fullName.value = "";
    router.push("/login");
  });

  navBasic.remove();
  navAdmin.classList.remove("zk-hidden");
  simpleHello.classList.remove("zk-hidden");

  loadModal();
}

function loadModal() {
  const cookieModal = getByID<HTMLDivElement>("zkCookieModal");
  const cookieBox = getByID<HTMLDivElement>("zkCookieBox");
  const cookieX = getByID<HTMLDivElement>("zkCookieX");
  const cookieOK = getByID<HTMLDivElement>("zkCookieOK");
  if (!cookieModal || !cookieBox || !cookieX || !cookieOK) return;

  if (allowCookies.value === true) {
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
    setTimeout(() => showCookiePopup(show), 50);
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

onMounted(() => {
  nextTick(() => {
    checkAuthorizations();
  });
});
</script>
<style>
.zk-nav-admin {
  background-color: #A1887F !important;
}
.zk-nav-admin a,
.zk-nav-admin span {
  color: #fff !important;
}
.zk-nav-admin .zk-nav-link:hover {
  background-color: rgba(255, 255, 255, 0.1) !important;
}
.zk-nav-admin .zk-nav-home:hover {
  background-color: rgba(255, 255, 255, 0.1) !important;
}
.zk-nav-admin .zk-nav-link:hover {
  background-color: rgba(255, 255, 255, 0.1) !important;
  cursor: pointer;
}
.zk-simple-hello {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 300px;
  padding: 20px;
  background: #fff;
  border-radius: 8px;
  border: 1px solid rgba(0, 0, 0, 0.1);
  box-shadow: 0 0 1px #000000bf;
}
</style>
