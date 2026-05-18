<template>
<client-only>
<div id="zkSignUpBox" class="zk-web-box zk-hidden">
<div class="zk-web-header">Sign Up</div>
<div class="zk-web-slogan">Make the world cleaner.</div>
<div id="zkSignUpForm" class="zk-web-form">
<input
id="zkSignUpFullName"
name="zkSignUpFullName"
type="text"
class="zk-web-input"
placeholder="Full name"
required
/>
<input
id="zkSignUpEmail"
name="zkSignUpEmail"
type="text"
class="zk-web-input"
placeholder="Email"
required
/>
<input
id="zkSignUpPassword"
name="zkSignUpPassword"
type="password"
class="zk-web-input"
placeholder="Password"
required
/>
</div>
<div id="zkSignUpMessage" class="zk-web-message zk-hidden">
Test message...
</div>
<div id="zkSignUpActions" class="zk-web-actions">
<div id="zkSignUpOK" class="zk-web-action zk-web-ok">Sign Up</div>
</div>
</div>
</client-only>
</template>