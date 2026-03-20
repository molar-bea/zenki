<template>
  <client-only>
    <div id="zkLoginBox" class="zk-login-box zk-hidden">
      <div class="zk-login-header">Zenki Login</div>
      <div class="zk-login-slogan">Enter your credentials below</div>
      
      <div id="zkLogInForm" class="zk-login-form">
        <input id="zkLoginUsername" class="zk-login-input" type="text" placeholder="Username" />
        <input id="zkLoginPassword" class="zk-login-input" type="password" placeholder="Password" />
      </div>

      <div id="zkLogInMessage" class="zk-login-message zk-hidden"></div>
      
      <div id="zkLogInActions" class="zk-login-actions">
        <div id="zkLoginOK" class="zk-login-action zk-login-ok" data-busy="0">Login</div>
      </div>
    </div>
  </client-only>
</template>

<script setup lang="ts">
</script>