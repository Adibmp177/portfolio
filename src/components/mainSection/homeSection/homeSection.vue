<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

// ── Typing animation ──────────────────────────────────────
const roles = [
  'UI/UX Designer',
  'Problem Solver',
  'Product Thinker',
  'Visual Storyteller',
  'User Advocate',
  'Interaction Designer',
];

const displayedRole = ref('');
let roleIndex = 0;
let charIndex = 0;
let isDeleting = false;
let typingTimer = null;

function typeEffect() {
  const currentRole = roles[roleIndex];

  if (!isDeleting) {
    displayedRole.value = currentRole.slice(0, charIndex + 1);
    charIndex++;
    if (charIndex === currentRole.length) {
      isDeleting = true;
      const pauseDuration = roleIndex === 0 ? 4000 : 1800;
      typingTimer = setTimeout(typeEffect, pauseDuration);
      return;
    }
  } else {
    displayedRole.value = currentRole.slice(0, charIndex - 1);
    charIndex--;
    if (charIndex === 0) {
      isDeleting = false;
      roleIndex = (roleIndex + 1) % roles.length;
    }
  }

  const speed = isDeleting ? 55 : 85;
  typingTimer = setTimeout(typeEffect, speed);
}

onMounted(() => {
  typingTimer = setTimeout(typeEffect, 900);
});
onUnmounted(() => {
  clearTimeout(typingTimer);
});
</script>

<template>

    <div class="homeWrapper">

        <p class="greeting">Hi, i'm</p>

        <h1 class="myName">Adib mohammad pouri</h1>

        <!-- Subtitle: "i'm a" is fixed/static, only the role text changes -->
        <p class="subtitle">
            <span class="subtitle-static">i'm a&nbsp;</span><span class="role">{{ displayedRole }}<span class="cursor">|</span></span>
        </p>

        <p class="intro">
            I design clean, purposeful interfaces for web and mobile. turning ideas into products
            people enjoy using, and businesses love to grow with.
        </p>

        <!-- CTA Buttons — Button Component -->
        <div class="homeButton--wrapper">

            <!-- Primary Fill: icon LEFT + label -->
            <a href="#Portfolio" class="cta-btn cta-btn--primary" id="hero-view-projects-btn">
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="btn-icon--left">
                    <path fill-rule="evenodd" d="M7.502 6h7.128A3.375 3.375 0 0 1 18 9.375v9.375a3 3 0 0 0 3-3V6.108c0-1.505-1.125-2.811-2.664-2.94a48.972 48.972 0 0 0-.673-.05A3 3 0 0 0 15 1.5h-1.5a3 3 0 0 0-2.663 1.618c-.225.015-.45.032-.673.05C8.662 3.295 7.554 4.542 7.502 6ZM13.5 3A1.5 1.5 0 0 0 12 4.5h4.5A1.5 1.5 0 0 0 15 3h-1.5Z" clip-rule="evenodd" />
                    <path fill-rule="evenodd" d="M3 9.375C3 8.339 3.84 7.5 4.875 7.5h9.75c1.036 0 1.875.84 1.875 1.875v11.25c0 1.035-.84 1.875-1.875 1.875h-9.75A1.875 1.875 0 0 1 3 20.625V9.375ZM6 12a.75.75 0 0 1 .75-.75h.008a.75.75 0 0 1 0 1.5H6.75A.75.75 0 0 1 6 12Zm2.25 0a.75.75 0 0 1 .75-.75h3.75a.75.75 0 0 1 0 1.5H9a.75.75 0 0 1-.75-.75Zm-2.25 3a.75.75 0 0 1 .75-.75h.008a.75.75 0 0 1 0 1.5H6.75A.75.75 0 0 1 6 15Zm2.25 0a.75.75 0 0 1 .75-.75h3.75a.75.75 0 0 1 0 1.5H9a.75.75 0 0 1-.75-.75Zm-2.25 3a.75.75 0 0 1 .75-.75h.008a.75.75 0 0 1 0 1.5H6.75A.75.75 0 0 1 6 18Zm2.25 0a.75.75 0 0 1 .75-.75h3.75a.75.75 0 0 1 0 1.5H9a.75.75 0 0 1-.75-.75Z" clip-rule="evenodd" />
                </svg>
                <span class="btn-label">View my Projects</span>
            </a>

            <!-- Outline: Contact me — fully transparent bg, gradient border -->
            <a href="#contact" class="cta-btn cta-btn--outline" id="hero-contact-btn">
                <span class="btn-label">Contact me</span>
            </a>
        </div>

        <!-- Social Icons -->
        <div class="social--wrapper">
            <!-- Figma -->
            <a href="https://www.figma.com/@adibmohammadpou" class="social-icon" aria-label="Figma" target="_blank" rel="noopener noreferrer">
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 38 57" fill="currentColor">
                    <path d="M19 28.5a9.5 9.5 0 1 1 19 0 9.5 9.5 0 0 1-19 0Z"/>
                    <path d="M0 47.5A9.5 9.5 0 0 1 9.5 38H19v9.5a9.5 9.5 0 0 1-19 0Z"/>
                    <path d="M19 0v19h9.5a9.5 9.5 0 0 0 0-19H19Z"/>
                    <path d="M0 9.5A9.5 9.5 0 0 0 9.5 19H19V0H9.5A9.5 9.5 0 0 0 0 9.5Z"/>
                    <path d="M0 28.5A9.5 9.5 0 0 0 9.5 38H19V19H9.5A9.5 9.5 0 0 0 0 28.5Z"/>
                </svg>
            </a>
            <!-- LinkedIn -->
            <a href="https://www.linkedin.com/in/adibmohammadpouri/" class="social-icon" aria-label="LinkedIn" target="_blank" rel="noopener noreferrer">
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor">
                    <path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433a2.062 2.062 0 0 1-2.063-2.065 2.064 2.064 0 1 1 2.063 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/>
                </svg>
            </a>
            <!-- Telegram -->
            <a href="https://t.me/Adibmohamadpori" class="social-icon" aria-label="Telegram" target="_blank" rel="noopener noreferrer">
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor">
                    <path d="M12 0C5.373 0 0 5.373 0 12s5.373 12 12 12 12-5.373 12-12S18.627 0 12 0Zm5.562 8.248-2.04 9.617c-.152.672-.554.836-1.123.52l-3.1-2.285-1.495 1.438c-.165.165-.304.304-.624.304l.223-3.167 5.754-5.195c.25-.223-.054-.347-.388-.124L7.29 14.806l-3.045-.953c-.663-.207-.677-.663.138-.98l11.893-4.585c.551-.199 1.033.134.857.98l-.571-.02Z"/>
                </svg>
            </a>
            <!-- Dribbble -->
            <a href="https://dribbble.com/adibmohammadpouri" class="social-icon" aria-label="Dribbble" target="_blank" rel="noopener noreferrer">
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor">
                    <path d="M12 2a10 10 0 1 0 10 10A10.011 10.011 0 0 0 12 2zm6.75 6.09a8.02 8.02 0 0 1 2.06 5.25c-.32-.05-3.83-.56-7.38-.07a41.87 41.87 0 0 0-.74-1.52c3.55-1.41 5.04-3.1 5.17-3.25a7.9 7.9 0 0 1 .89-.41zm-1.82-.77c-.12.14-1.49 1.7-4.85 3.01a45.69 45.69 0 0 0-3.3-4.94A8.07 8.07 0 0 1 12 4a7.94 7.94 0 0 1 4.93 1.32zM8.34 2.8a44.62 44.62 0 0 1 3.23 4.88c-3.79 1.05-7.14 1.04-7.5 1.04a7.99 7.99 0 0 1 4.27-5.92zm-5.18 7.4c.39 0 3.38.01 7.02-.97.26.51.51 1.03.75 1.55-3.84 1.09-7.34 1.57-7.69 1.62a8.04 8.04 0 0 1-.08-2.2zm1.2 3.81c.32-.04 3.49-.49 7.15-1.53.86 2.37 1.37 4.74 1.54 5.67A8.02 8.02 0 0 1 4.36 14.01zm9.4 6.8c-.18-.97-.66-3.28-1.5-5.59 3.3-.43 6.55.03 6.87.08a8.02 8.02 0 0 1-5.37 5.51z"/>
                </svg>
            </a>
        </div>

    </div>

    <a href="#aboutMe" class="scrollDown" aria-label="Scroll down">
        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" d="m4.5 5.25 7.5 7.5 7.5-7.5m-15 6 7.5 7.5 7.5-7.5" />
        </svg>
    </a>

</template>

<style scoped>

/* ─── Scroll Down ────────────────────────────────────── */
.scrollDown {
    display: inline-block;
    position: absolute;
    bottom: 28px;
    left: 50%;
    transform: translate(-50%, 0);
    width: 42px;
    padding: 5px;
    color: rgba(255,255,255,0.4);
    animation: moving 0.9s alternate infinite ease-in-out;
    opacity: 0;
    transition: opacity 0.5s 1.2s;
}
.active--s .scrollDown { opacity: 1; }
@keyframes moving {
    0%   { transform: translate(-50%, 0px); }
    100% { transform: translate(-50%, -12px); }
}

/* ─── Wrapper ────────────────────────────────────────── */
.homeWrapper {
    text-align: center;
    color: var(--main-txt);
    padding-top: 40px;
    display: flex;
    flex-direction: column;
    align-items: center;
}

/* ─── Greeting ───────────────────────────────────────── */
.greeting {
    font-family: var(--font-body);
    font-size: 16px;
    font-weight: 400;
    color: rgba(255, 255, 255, 0.6);
    letter-spacing: 0.3px;
    margin-bottom: 12px;
    opacity: 0;
    transform: translateY(18px);
    transition: opacity 0.7s 0.1s ease-out, transform 0.7s 0.1s ease-out;
}
.active--s .greeting { opacity: 1; transform: translateY(0); }

/* ─── Name — gradient text ───────────────────────────── */
.myName {
    font-family: var(--font-display);
    font-weight: 700;
    font-size: clamp(34px, 5.5vw, 68px);
    line-height: 1.08;
    letter-spacing: -0.5px;
    margin-bottom: 20px;
    opacity: 0;
    transform: translateY(22px);
    transition: opacity 0.85s 0.2s ease-out, transform 0.85s 0.2s ease-out;
    background: linear-gradient(90deg, #6c63ff 0%, #9b59f5 100%);
    -webkit-background-clip: text;
    background-clip: text;
    color: transparent;
}
.active--s .myName { opacity: 1; transform: translateY(0); }

/* ─── Subtitle ───────────────────────────────────────── */
/* 
  Layout: row, left-aligned items
  "i'm a " is static/fixed, role text grows from it left→right
*/
.subtitle {
    font-family: var(--font-body);
    font-size: 18px;
    font-weight: 400;
    color: rgba(255, 255, 255, 0.7);
    margin-bottom: 24px;
    opacity: 0;
    transform: translateY(18px);
    transition: opacity 0.85s 0.32s ease-out, transform 0.85s 0.32s ease-out;
    /* Flex row — "i'm a" anchored, role expands to the right */
    display: flex;
    align-items: baseline;
    justify-content: center;
    min-height: 28px;
    white-space: nowrap;
}
.active--s .subtitle { opacity: 1; transform: translateY(0); }

/* Static part — never moves */
.subtitle-static {
    flex-shrink: 0;
}

/* Role span: fixed width = widest possible role, text left-aligned inside
   This prevents "i'm a" from shifting when text gets shorter */
.role {
    font-weight: 600;
    background: linear-gradient(90deg, #6c63ff 0%, #9b59f5 100%);
    -webkit-background-clip: text;
    background-clip: text;
    color: transparent;
    display: inline-block;
}

/* Blinking cursor */
.cursor {
    display: inline;
    color: #9b59f5;
    font-weight: 300;
    margin-left: 1px;
    animation: blink 1s step-end infinite;
    background: none;
    -webkit-background-clip: unset;
    background-clip: unset;
}
@keyframes blink {
    0%, 100% { opacity: 1; }
    50%       { opacity: 0; }
}

/* ─── Intro ──────────────────────────────────────────── */
.intro {
    font-family: var(--font-body);
    font-size: 15px;
    font-weight: 400;
    line-height: 1.8;
    max-width: 500px;
    color: rgba(255, 255, 255, 0.5);
    margin-bottom: 44px;
    opacity: 0;
    transform: translateY(22px);
    transition: opacity 0.85s 0.44s ease-out, transform 0.85s 0.44s ease-out;
}
.active--s .intro { opacity: 1; transform: translateY(0); }

/* ═══════════════════════════════════════════════════════
   BUTTON COMPONENT  —  Figma Design System
   
   Fill button:
   - Default: gradient left #6c63ff → right #9b59f5
   - Hover:   gradient sweeps — purple (#9b59f5) slides from right to left
     Technique: oversized gradient background + background-position shift
   
   Outline button:
   - Background: fully transparent (no fill at all)  
   - Border: 1.5px solid using gradient-border technique
   - Text: white (#fff)
════════════════════════════════════════════════════════ */
.homeButton--wrapper {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 14px;
    margin-bottom: 48px;
    opacity: 0;
    transform: translateY(22px);
    transition: opacity 0.85s 0.56s ease-out, transform 0.85s 0.56s ease-out;
}
.active--s .homeButton--wrapper { opacity: 1; transform: translateY(0); }

/* ── Base ── */
.cta-btn {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
    padding: 13px 28px;
    border-radius: 50px;
    font-family: var(--font-body);
    font-size: 15px;
    font-weight: 500;
    letter-spacing: 0.2px;
    cursor: pointer;
    text-decoration: none;
    border: none;
    outline: none;
    position: relative;
    overflow: hidden;
    user-select: none;
    -webkit-tap-highlight-color: transparent;
}

/* ── Fill / Primary button ──
   Uses a wide gradient (200% width) and slides background-position on hover
   This creates the smooth "sweep from right to left" effect described in Figma */
.cta-btn--primary {
    color: #fff;
    background: linear-gradient(90deg, #6c63ff 0%, #9b59f5 50%, #6c63ff 100%);
    background-size: 200% 100%;
    background-position: left center;
    box-shadow: 0 4px 20px rgba(108, 99, 255, 0.4);
    transition:
        background-position 0.55s ease,
        box-shadow          0.3s ease,
        transform           0.2s ease;
}
.cta-btn--primary:hover {
    background-position: right center;
    box-shadow: 0 8px 28px rgba(155, 89, 245, 0.55);
    transform: translateY(-3px);
}
.cta-btn--primary:active {
    transform: translateY(1px) scale(0.97);
    box-shadow: 0 3px 12px rgba(108, 99, 255, 0.35);
}

/* Children sit above any future pseudo-layers */
.btn-icon--left,
.btn-label {
    position: relative;
    z-index: 1;
}

/* Left icon */
.btn-icon--left {
    width: 18px;
    height: 18px;
    flex-shrink: 0;
    color: currentColor;
}

/* ── Outline pill ──
   Figma spec: blue text + blue border (default), purple text + purple border + subtle bg (hover) */
.cta-btn--outline {
    color: #6c63ff;
    background: transparent;
    border: 1.5px solid #6c63ff;
    box-shadow: none;
    transition:
        color        0.3s ease,
        border-color 0.3s ease,
        background   0.3s ease,
        box-shadow   0.3s ease,
        transform    0.2s ease;
}
.cta-btn--outline:hover {
    color: #9b59f5;
    border-color: #9b59f5;
    background: rgba(108, 99, 255, 0.1);
    box-shadow: 0 0 0 1px rgba(155, 89, 245, 0.2),
                0 6px 22px rgba(108, 99, 255, 0.15);
    transform: translateY(-3px);
}
.cta-btn--outline:active {
    transform: translateY(1px) scale(0.97);
    border-color: #6c63ff;
    color: #6c63ff;
    background: rgba(108, 99, 255, 0.08);
}

/* ─── Social Icons ──────────────────────────────────── */
.social--wrapper {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 12px;
    opacity: 0;
    transform: translateY(16px);
    transition: opacity 0.85s 0.7s ease-out, transform 0.85s 0.7s ease-out;
}
.active--s .social--wrapper { opacity: 1; transform: translateY(0); }

.social-icon {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 42px;
    height: 42px;
    border-radius: 50%;
    color: rgba(255, 255, 255, 0.55);
    border: 1.5px solid rgba(255, 255, 255, 0.12);
    background: rgba(255, 255, 255, 0.03);
    transition:
        color        0.22s ease,
        border-color 0.22s ease,
        background   0.22s ease,
        box-shadow   0.22s ease,
        transform    0.22s ease;
}
.social-icon svg { width: 19px; height: 19px; }

.social-icon:hover {
    color: #fff;
    border-color: rgba(108, 99, 255, 0.65);
    background: rgba(108, 99, 255, 0.18);
    box-shadow: 0 6px 20px rgba(108, 99, 255, 0.3);
    transform: translateY(-3px);
}
.social-icon:active {
    transform: translateY(0) scale(0.93);
}

/* ─── Responsive ─────────────────────────────────────── */
@media screen and (max-width: 768px) {
    .homeWrapper { padding-top: 20px; }
    .myName { font-size: 36px; }
    .subtitle { font-size: 16px; }
    .intro { font-size: 14px; max-width: 88%; }
    .cta-btn { padding: 11px 22px; font-size: 14px; }
}

@media screen and (max-width: 450px) {
    .homeButton--wrapper { flex-direction: column; gap: 10px; width: 100%; }
    .cta-btn { width: 82%; justify-content: center; }
    .myName { font-size: 28px; }
    .intro { max-width: 96%; }
    .subtitle { white-space: normal; flex-wrap: wrap; }
}

</style>