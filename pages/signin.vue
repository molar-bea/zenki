<template>
  <client-only>
    <NavBar :navAdminMode="navAdminMode" />
    <div id="zkMain" class="zk-main">
      <SignIn />
    </div>
    <Cookies />
    <Copyright />
  </client-only>
</template>
<script setup lang="ts">
import { useSeoMeta, useHead } from "@vueuse/head";
import '../public/custom.css'

const title = "Zenki";
const description = "Helps systematize admission processes.";
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
      href: "https://fonts.googleapis.com/css2?family=Noto+Sans:ital,wght@0,100..900;1,100..900&family=Winky+Sans:ital,wght@0,300..900;1,300..900&display=swap",
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
let lastSignInClicked = 0;
const router = useRouter();
const navAdminMode = computed(() =>
  userLevel.value >= 2 ? "zk-nav-admin" : "",
);
const zkServer = "https://zenki-api.vercel.app";
type AuthResponse = {
  success: number;
  accessToken: string;
  userLevel: number;
  message: string;
};
function getByID<T extends HTMLElement>(id: string) {
  return document.getElementById(id) as T | null;
}
function checkAuthorizations() {
  if (accessToken.value) {
    if (userLevel.value <= 1) {
      router.push("/");
    } else if (userLevel.value >= 2) {
      router.push("/admin");
    }
  }
  const signinBox = getByID<HTMLDivElement>("zkSignInBox");
  const signinEmail = getByID<HTMLInputElement>("zkSignInEmail");
  const signinPassword = getByID<HTMLInputElement>("zkSignInPassword");
  const signinMessage = getByID<HTMLDivElement>("zkSignInMessage");
  const signinOK = getByID<HTMLDivElement>("zkSignInOK");
  if (
    !signinBox ||
    !signinEmail ||
    !signinPassword ||
    !signinMessage ||
    !signinOK
  )
    return;
  signinBox.classList.remove("zk-hidden");
  signinOK.addEventListener("click", () => {
    if (signinOK.dataset.busy == "1") return;
    const tempEmail = signinEmail.value;
    const tempPassword = signinPassword.value;
    if (!tempEmail) {
      signinMessage.innerText = "Email is required.";
      signinMessage.classList.remove("zk-hidden");
      return;
    }
    if (!tempPassword) {
      signinMessage.innerText = "Password is required.";
      signinMessage.classList.remove("zk-hidden");
      return;
    }
    signInWithPassword(tempEmail, tempPassword);
  });
  signinEmail.addEventListener("keyup", (e) => {
    if (e.key === "Enter" && signinEmail.value) {
      signinPassword.focus();
    }
  });
  signinPassword.addEventListener("keyup", (e) => {
    if (e.key === "Enter") signinOK.click();
  });
  loadModal();
}
async function signInWithPassword(tempEmail: string, tempPassword: string) {
  if (lastSignInClicked >= Date.now() - globalDelay) return;
  lastSignInClicked = Date.now();
  const signinEmail = getByID<HTMLInputElement>("zkSignInEmail");
  const signinPassword = getByID<HTMLInputElement>("zkSignInPassword");
  const signinMessage = getByID<HTMLDivElement>("zkSignInMessage");
  const signinOK = getByID<HTMLDivElement>("zkSignInOK");
  if (!signinEmail || !signinPassword || !signinOK || !signinMessage) return;
  let isSuccessful = false;
  signinMessage.innerText = "";
  signinMessage.classList.add("zk-hidden");
  [signinEmail, signinPassword].forEach((el) => (el.disabled = true));
  signinOK.dataset.busy = "1";
  try {
    const response = (await $fetch(`${zkServer}/signin`, {
      headers: { "Content-Type": "application/json" },
      method: "POST",
      body: {
        email: tempEmail,
        password: tempPassword,
      },
    })) as AuthResponse;
    isSuccessful = Boolean(response.success === 1);
    emailAddress.value = tempEmail;
    accessToken.value = response.accessToken;
    userLevel.value = response.userLevel;
    if (response.message) {
      signinMessage.innerText = response.message;
      signinMessage.classList.remove("zk-hidden");
    }
  } catch (e: any) {
    signinMessage.innerText = `Error encountered: ${e}`;
    signinMessage.classList.remove("zk-hidden");
  } finally {
    signinOK.dataset.busy = "0";
  }
  [signinEmail, signinPassword].forEach((el) => {
    el.remove();
  });
  signinOK.dataset.busy = "0";
  if (isSuccessful) {
    router.push("/");
  }
}
function loadModal() {
  const cookieX = getByID<HTMLDivElement>("zkCookieX");
  const cookieOK = getByID<HTMLDivElement>("zkCookieOK");
  if (!cookieX || !cookieOK) return;
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
  if (!cookieBox || !cookieModal) return;
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
  nextTick(checkAuthorizations);
});
</script>
