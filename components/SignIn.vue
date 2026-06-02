<template>
  <client-only>
    <div id="zkSignInBox" class="zk-web-box zk-hidden">
      <div class="zk-web-header">Sign In</div>
      <div class="zk-web-slogan">Helps systematize admission processes.</div>
      <div id="zkSignInForm" class="zk-web-form">
        <input
          id="zkSignInEmail"
          name="zkSignInEmail"
          type="text"
          class="zk-web-input"
          placeholder="Email"
          required
        />
        <input
          id="zkSignInPassword"
          name="zkSignInPassword"
          type="password"
          class="zk-web-input"
          placeholder="Password"
          required
        />
      </div>
      <div id="zkSignInMessage" class="zk-web-zk-hidden">Test message...</div>
      <div id="zkSignInActions" class="zk-web-actions">
        <div id="zkSignInOK" class="zk-web-action zk-web-ok">Sign In</div>
      </div>
    </div>
  </client-only>
</template>
