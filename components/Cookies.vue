<template>
    <client-only>
        <div id="zkCookieModal" class="zk-cookie-modal bh-hidden"></div>
        <div id="zkCookieBox" class="zk-cookie-box bh-hidden">
        <span id="zkCookieX" class="zk-cookie-x">✕</span>
        <div class="zk-cookie-header" >Cookies and Privacy</div>
        <div class="zk-cookie-message">
            We use cookies to ensure you get the best experience on our website.
        </div>
        <div class="zk-cookie-actions">
            <a href="/policy" class="zk-cookie-link" target="_blank">
                <div class="zk-cookie-action zk-cookie-more">Read more</div>
            </a>
        </div>
        <div id="zkCookieOK" class="zk-cookie-action zk-cookie-ok">Accept all</div>
        </div>
    </client-only>
</template>