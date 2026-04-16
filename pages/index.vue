<script  lang="ts"></script>
<template>
  <client-only>
    <NavBar :navAdminMode="navAdminMode" />
    <div id="zkMain" class="zk-main">
      <span id="zkPageTitle" class="zk-page-title zk-hidden">Latest</span>
      <div id="zkContainer" class="zk-container"></div>
    </div>
    <Cookies />
    <AboutUs />
    <Copyright />
  </client-only>
</template>

<script setup lang="ts">
import { useSeoMeta, useHead } from "@vueuse/head";

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

const globalDelay = 500;

const allowCookies = useCookie<boolean>("allowCookies", {
  sameSite: "none",
  secure: true,
  maxAge: 60 * 60 * 24,
});

//allowCookies.value =false;
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

type ContentItem = {
  id: string;
  author: string;
  title: string;
  content: string;
  isSynchronized: number;
  createdAt: number;
};

type ContentResponse = {
  contents: ContentItem[];
};

const router = useRouter();
const zkServer = "https://zenki-api.vercel.app";
let navAdminMode = userLevel.value >= 2 ? "zk-nav-admin" : "";

function getByID<T extends HTMLElement>(id: string) {
  return document.getElementById(id) as T;
}

function checkAuthorizations() {
  if (!accessToken.value) {
    router.push("/login");
  } else if (userLevel.value >= 2) {
    router.push("/admin");
  }

  const navBasic = getByID<HTMLDivElement>("zkNavBasic");
  const navAdmin = getByID<HTMLDivElement>("zkNavAdmin");
  const navLogout = getByID<HTMLDivElement>("zkNavBasicLogout");
  const pageTitle = getByID<HTMLSpanElement>("zkPageTitle");

  if (!navBasic || !navAdmin || !navLogout || !pageTitle) return;

  navLogout.addEventListener("click", (e) => {
    retries.value = 0;
    username.value = "";
    accessToken.value = "";
    userLevel.value = -1;
    fullName.value = "";

    router.push("/login");
  });

  navAdmin.remove();
  navBasic.classList.remove("zk-hidden");
  pageTitle.classList.remove("zk-hidden");

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
  loadContents();
}

onMounted(() => {
  nextTick(() => {
    checkAuthorizations();
  });
});

async function loadContents() {
  if (!accessToken.value) return;
  var rawContents = [] as ContentItem[];
  try {
    const query = new URLSearchParams({
      username: username.value,
      userLevel: String(userLevel.value),
      accessToken: accessToken.value,
    }).toString();
    const response = (await $fetch(`${zkServer}/get_contents?${query}`, {
      headers: { "Content-Type": "application/json" },
      method: "GET",
    })) as ContentResponse;
    rawContents = response.contents;
  } catch (e: any) {
    return;
  }

  const container = getByID<HTMLDivElement>("zkContainer");
  if (!container) return;

  container.innerHTML = "";
  const contents = renderContents(rawContents) as HTMLElement;
  container.appendChild(contents);
}

function renderContents(data: ContentItem[]): HTMLElement {
  const parent = document.createElement("div");
  parent.className = "zk-contents";

  data.forEach((item, index) => {
    const wrapper = document.createElement("div");
    wrapper.id = `content-${index}`;
    wrapper.className = "zk-content-box";
    const title = document.createElement("h2");
    title.className = "zk-content-title";
    title.textContent = item.title;
    const meta = document.createElement("p");
    const date = new Date(item.createdAt * 1000);
    const published = date.toLocaleDateString("en-US", {
      year: "numeric",
      month: "long",
      day: "numeric",
    });

    meta.textContent = `by ${item.author} • ${published}`;
    meta.className = "zk-content-meta";

    const content = document.createElement("p");
    content.className = "zk-content-data";
    content.textContent = item.content;

    wrapper.append(title, meta, content);
    parent.appendChild(wrapper);
  });

  return parent;
}
</script>

<style>
.zk-nav-link:hover {
  cursor: pointer;
}

.zk-page-title {
  position: relative;
  margin: 60px auto 0;
  width: 800px;
  max-width: 90%;
  padding: 20px;
  font-size: 1.8em;
  font-weight: bold;
  border-bottom: 1px solid rgba(0, 0, 0, 0.2);
  display: block;
}

.zk-container {
  position: relative;
  margin: 20px auto 0;
  width: 800px;
  max-width: 90%;
}

.zk-content-box {
  margin-bottom: 10px;
  padding: 20px;
  background: #fff;
  border-radius: 3px;
  border: 1px solid rgba(0, 0, 0, 0.2);
  cursor: pointer;
}

.zk-content-title {
  line-height: 1.5em;
  font-weight: bold;
}

.zk-content-meta {
  font-size: 0.8em;
  color: #666;
}

.zk-content-data {
  margin-top: 10px;
  line-height: 1.5em;
}
</style>
