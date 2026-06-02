<template>
<client-only>
<NavBar :navAdminMode="navAdminMode" />
<div id="zkMain" class="zk-main">
<SignUp />
</div>
<Cookies />
<Copyright />
</client-only>
</template>
<script setup lang="ts">
import { useSeoMeta, useHead } from "@vueuse/head";
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
const accessToken = useCookie<string>("accessToken", cookieOptions);
accessToken.value = accessToken.value ?? "";
const userLevel = useCookie<number>("userLevel", cookieOptions);
userLevel.value = userLevel.value ?? -1;
let lastSignUpClicked = 0;
const router = useRouter();
const navAdminMode = computed(() =>
userLevel.value >= 2 ? "zk-nav-admin" : "",
);
const zkServer = "https://zenki-api.vercel.app";
type AuthResponse = {
success: number;
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
const signupBox = getByID<HTMLDivElement>("zkSignUpBox");
const signupFullName = getByID<HTMLInputElement>("zkSignUpFullName");
const signupEmail = getByID<HTMLInputElement>("zkSignUpEmail");
const signupPassword = getByID<HTMLInputElement>("zkSignUpPassword");
const signupMessage = getByID<HTMLDivElement>("zkSignUpMessage");
const signupOK = getByID<HTMLDivElement>("zkSignUpOK");
if (
!signupBox ||
!signupFullName ||
!signupEmail ||
!signupPassword ||
!signupMessage ||
!signupOK
)
return;
signupBox.classList.remove("zk-hidden");
signupOK.addEventListener("click", () => {
if (signupOK.dataset.busy == "1") return;
const tempFullName = signupFullName.value;
const tempEmail = signupEmail.value;
const tempPassword = signupPassword.value;
if (!tempFullName) {
signupMessage.innerText = "Full name is required";
signupMessage.classList.remove("zk-hidden");
return;
}
if (!tempEmail) {
signupMessage.innerText = "Fix email address format.";
signupMessage.classList.remove("zk-hidden");
return;
}
if (!tempPassword) {
signupMessage.innerText =
"Password must be 8–16 characters; contains at least 1 uppercase, lowercase, digit, and symbol.";
signupMessage.classList.remove("zk-hidden");
return;
}
createNewUser(tempFullName, tempEmail, tempPassword);
});
signupFullName.addEventListener("keyup", (e) => {
if (e.key === "Enter" && signupFullName.value) {
signupEmail.focus();
}
});
signupEmail.addEventListener("keyup", (e) => {
if (e.key === "Enter" && signupEmail.value) {
signupPassword.focus();
}
});
signupPassword.addEventListener("keyup", (e) => {
if (e.key === "Enter") signupOK.click();
});
loadModal();
}
async function createNewUser(
tempFullName: string,
tempEmail: string,
tempPassword: string,
) {
if (lastSignUpClicked >= Date.now() - globalDelay) return;
lastSignUpClicked = Date.now();
const signupFullName = getByID<HTMLInputElement>("zkSignUpFullName");
const signupEmail = getByID<HTMLInputElement>("zkSignUpEmail");
const signupPassword = getByID<HTMLInputElement>("zkSignUpPassword");
const signupMessage = getByID<HTMLDivElement>("zkSignUpMessage");
const signupOK = getByID<HTMLDivElement>("zkSignUpOK");
if (
!signupFullName ||
!signupEmail ||
!signupPassword ||
!signupOK ||
!signupMessage
)
return;
let isSuccessful = false;
signupMessage.innerText = "";
signupMessage.classList.add("zk-hidden");
[signupFullName, signupEmail, signupPassword].forEach(
(el) => (el.disabled = true),
);
signupOK.dataset.busy = "1";
try {
const response = (await $fetch(`${zkServer}/signup`, {
headers: { "Content-Type": "application/json" },
method: "POST",
body: {
fullName: tempFullName,
email: tempEmail,
password: tempPassword,
},
})) as AuthResponse;
isSuccessful = Boolean(response.success === 1);
if (response.message) {
signupMessage.innerText = response.message;
signupMessage.classList.remove("zk-hidden");
}
} catch (e: any) {
signupMessage.innerText = `Error encountered: ${e}`;
signupMessage.classList.remove("zk-hidden");
} finally {
signupOK.dataset.busy = "0";
}
[signupFullName, signupEmail, signupPassword].forEach(
(el) => (el.disabled = false),
);
signupOK.dataset.busy = "0";
if (isSuccessful) {
[signupFullName, signupEmail, signupPassword, signupOK].forEach((el) =>
el.classList.add("zk-hidden"),
);
signupMessage.innerText = "Sign in after email confirmation is received.";
signupMessage.classList.remove("zk-hidden");
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