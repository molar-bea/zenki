<template>
  <client-only>
    <header :class="['zk-navbar', navAdminMode]">
      <nav class="zk-nav-left">
        <a href="/" class="zk-nav-home">
          <img src="/logo.png" width="20" height="20" class="zk-nav-logo" />
          <span>Zenki</span>
        </a>
      </nav>
      <nav id="zkNavBasic" class="zk-nav-right zk-hidden">
        <ul>
          <li><a href="#" class="zk-nav-link">Checklist</a></li>
          <li><a href="#" class="zk-nav-link">Appointments</a></li>
          <li><a href="#" class="zk-nav-link">Guide</a></li>
          <li><span id="zkNavBasicLogout" class="zk-nav-link">Logout</span></li>
        </ul>
      </nav>
          <nav id="zkNavGuest" class="zk-nav-right">
    <ul>
    <li><a href="/signup" class="zk-nav-link">Sign up</a></li>
    <li><a href="/signin" class="zk-nav-link">Sign in</a></li>
    </ul>
    </nav>
      <nav id="zkNavAdmin" class="zk-nav-right zk-hidden">
        <ul>
          <li><a href="#" class="zk-nav-link">Settings</a></li>
          <li><a href="#" class="zk-nav-link">Reports</a></li>
          <li><span id="zkNavAdminLogout" class="zk-nav-link">Logout</span></li>
        </ul>
      </nav>
    </header>
  </client-only>
</template>
<script setup lang="ts">
const props = defineProps<{ navAdminMode: string }>();
</script>
