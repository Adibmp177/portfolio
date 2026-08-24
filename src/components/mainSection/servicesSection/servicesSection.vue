<script setup>
import { onMounted, ref, onUnmounted } from 'vue';

// Animated counters for skill percentages
const figmaPercent = ref(0);
const psPercent = ref(0);
const aiPercent = ref(0);
let animFrame = null;

function animateCounters() {
    const targets = { figma: 100, ps: 75, ai: 85 };
    const duration = 1800;
    const start = performance.now();

    function tick(now) {
        const elapsed = now - start;
        const progress = Math.min(elapsed / duration, 1);
        // Ease out cubic
        const ease = 1 - Math.pow(1 - progress, 3);

        figmaPercent.value = Math.round(targets.figma * ease);
        psPercent.value = Math.round(targets.ps * ease);
        aiPercent.value = Math.round(targets.ai * ease);

        if (progress < 1) {
            animFrame = requestAnimationFrame(tick);
        }
    }
    animFrame = requestAnimationFrame(tick);
}

onMounted(() => {
    const Observer = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
            if (entry.isIntersecting) {
                entry.target.classList.add('active--s');

                // Stagger skill cards
                const cards = entry.target.querySelectorAll('.sk-card');
                cards.forEach((card, i) => {
                    setTimeout(() => card.classList.add('sk-card--visible'), 200 + i * 220);
                });

                // Stagger tag pills after cards
                const pills = entry.target.querySelectorAll('.tag-pill');
                pills.forEach((pill, i) => {
                    setTimeout(() => pill.classList.add('pill--visible'), 900 + i * 55);
                });

                // Start counter animation
                setTimeout(animateCounters, 400);

                Observer.unobserve(entry.target);
            }
        });
    }, {
        rootMargin: '-10% 0px -10% 0px'
    });

    let skillsItems = document.querySelector('.skills--wrapper');
    if (skillsItems) Observer.observe(skillsItems);
});

onUnmounted(() => {
    if (animFrame) cancelAnimationFrame(animFrame);
});
</script>

<template>
    <div class="skills--wrapper">
        <div class="container">

            <!-- Section Heading -->
            <div class="heading--wrapper">
                <h2 class="heading">My Skills</h2>
            </div>

            <!-- Skills Bento Grid -->
            <div class="sk-grid">

                <!-- ─── Card 1: Figma (Featured / Large) ─── -->
                <div class="sk-card sk-card--featured">

                    <div class="sk-card__inner">
                        <div class="sk-card__left">
                            <div class="sk-icon-anchor">
                                <div class="sk-glow sk-glow--figma"></div>
                                <div class="sk-icon-orb sk-icon-orb--figma">
                                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round">
                                        <path d="M5 5.5A3.5 3.5 0 0 1 8.5 2H12v7H8.5A3.5 3.5 0 0 1 5 5.5z"/>
                                        <path d="M12 2h3.5a3.5 3.5 0 1 1 0 7H12V2z"/>
                                        <path d="M12 12.5a3.5 3.5 0 1 1 7 0 3.5 3.5 0 1 1-7 0z"/>
                                        <path d="M5 19.5A3.5 3.5 0 0 1 8.5 16H12v3.5a3.5 3.5 0 1 1-7 0z"/>
                                        <path d="M5 12.5A3.5 3.5 0 0 1 8.5 9H12v7H8.5A3.5 3.5 0 0 1 5 12.5z"/>
                                    </svg>
                                </div>
                            </div>
                            <div class="sk-card__meta">
                                <h3 class="sk-card__title">Figma</h3>
                                <span class="sk-card__level sk-card__level--figma">Advanced</span>
                            </div>
                            <p class="sk-card__desc">
                                My primary design tool, crafting interfaces, interactive prototypes, 
                                and scalable design systems from concept to developer handoff.
                            </p>
                        </div>
                        <div class="sk-card__right">
                            <div class="sk-ring">
                                <svg viewBox="0 0 120 120" class="sk-ring__svg">
                                    <circle cx="60" cy="60" r="52" class="sk-ring__track" />
                                    <circle cx="60" cy="60" r="52" class="sk-ring__fill sk-ring__fill--figma" 
                                        :style="{ strokeDashoffset: 326.7 - (326.7 * figmaPercent / 100) }" />
                                </svg>
                                <span class="sk-ring__value">{{ figmaPercent }}<small>%</small></span>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- ─── Card 2: Photoshop ─── -->
                <div class="sk-card">

                    <div class="sk-card__inner sk-card__inner--vertical">
                        <div class="sk-card__top-row">
                            <div class="sk-icon-anchor">
                                <div class="sk-glow sk-glow--ps"></div>
                                <div class="sk-icon-orb sk-icon-orb--ps">
                                    <span>Ps</span>
                                </div>
                            </div>
                            <div class="sk-ring sk-ring--sm">
                                <svg viewBox="0 0 120 120" class="sk-ring__svg">
                                    <circle cx="60" cy="60" r="52" class="sk-ring__track" />
                                    <circle cx="60" cy="60" r="52" class="sk-ring__fill sk-ring__fill--ps" 
                                        :style="{ strokeDashoffset: 326.7 - (326.7 * psPercent / 100) }" />
                                </svg>
                                <span class="sk-ring__value sk-ring__value--sm">{{ psPercent }}<small>%</small></span>
                            </div>
                        </div>
                        <div class="sk-card__meta">
                            <h3 class="sk-card__title">Photoshop</h3>
                            <span class="sk-card__level sk-card__level--ps">Intermediate</span>
                        </div>
                        <p class="sk-card__desc">
                            Photo editing, compositing, and visual asset creation for polished mockups and presentations.
                        </p>
                    </div>
                </div>

                <!-- ─── Card 3: AI & Prompting ─── -->
                <div class="sk-card">

                    <div class="sk-card__inner sk-card__inner--vertical">
                        <div class="sk-card__top-row">
                            <div class="sk-icon-anchor">
                                <div class="sk-glow sk-glow--ai"></div>
                                <div class="sk-icon-orb sk-icon-orb--ai">
                                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor">
                                        <path stroke-linecap="round" stroke-linejoin="round" d="M9.813 15.904 9 18.75l-.813-2.846a4.5 4.5 0 0 0-3.09-3.09L2.25 12l2.846-.813a4.5 4.5 0 0 0 3.09-3.09L9 5.25l.813 2.846a4.5 4.5 0 0 0 3.09 3.09l2.846.813-2.846.813a4.5 4.5 0 0 0-3.09 3.09ZM18.259 8.715 18 9.75l-.259-1.035a3.375 3.375 0 0 0-2.455-2.456L14.25 6l1.036-.259a3.375 3.375 0 0 0 2.455-2.456L18 2.25l.259 1.035a3.375 3.375 0 0 0 2.456 2.456L21.75 6l-1.035.259a3.375 3.375 0 0 0-2.456 2.456ZM16.894 20.567 16.5 21.75l-.394-1.183a2.25 2.25 0 0 0-1.423-1.423L13.5 18.75l1.183-.394a2.25 2.25 0 0 0 1.423-1.423l.394-1.183.394 1.183a2.25 2.25 0 0 0 1.423 1.423l1.183.394-1.183.394a2.25 2.25 0 0 0-1.423 1.423Z" />
                                    </svg>
                                </div>
                            </div>
                            <div class="sk-ring sk-ring--sm">
                                <svg viewBox="0 0 120 120" class="sk-ring__svg">
                                    <circle cx="60" cy="60" r="52" class="sk-ring__track" />
                                    <circle cx="60" cy="60" r="52" class="sk-ring__fill sk-ring__fill--ai" 
                                        :style="{ strokeDashoffset: 326.7 - (326.7 * aiPercent / 100) }" />
                                </svg>
                                <span class="sk-ring__value sk-ring__value--sm">{{ aiPercent }}<small>%</small></span>
                            </div>
                        </div>
                        <div class="sk-card__meta">
                            <h3 class="sk-card__title">AI & Prompting</h3>
                            <span class="sk-card__level sk-card__level--ai">Proficient</span>
                        </div>
                        <p class="sk-card__desc">
                            Leveraging AI for rapid research, ideation, and prototyping to make design workflows faster and smarter.
                        </p>
                        <div class="sk-tools">
                            <span class="sk-tool">Claude</span>
                            <span class="sk-tool">Gemini</span>
                            <span class="sk-tool">Figma AI</span>
                            <span class="sk-tool">Stitch</span>
                        </div>
                    </div>
                </div>

            </div>

            <!-- Additional Skills -->
            <div class="sk-extra">
                <h3 class="sk-extra__title">Additional Skills</h3>

                <!-- UI/UX Related -->
                <div class="sk-category">
                    <h4 class="sk-category__label">UI/UX Related</h4>
                    <div class="sk-tags">
                        <span class="tag-pill">Design Systems</span>
                        <span class="tag-pill">Components</span>
                        <span class="tag-pill">Prototyping</span>
                        <span class="tag-pill">Wireframing</span>
                        <span class="tag-pill">User Research</span>
                        <span class="tag-pill">Usability Testing</span>
                        <span class="tag-pill">Information Architecture</span>
                        <span class="tag-pill">Handoff to Developers</span>
                    </div>
                </div>

                <!-- Soft Skills -->
                <div class="sk-category">
                    <h4 class="sk-category__label">Soft Skills</h4>
                    <div class="sk-tags">
                        <span class="tag-pill">Empathy</span>
                        <span class="tag-pill">Problem Solving</span>
                        <span class="tag-pill">Time Manager</span>
                        <span class="tag-pill">Team-Work</span>
                        <span class="tag-pill">Communication</span>
                    </div>
                </div>

                <!-- Programming -->
                <div class="sk-category">
                    <h4 class="sk-category__label">Programming</h4>
                    <div class="sk-tags">
                        <span class="tag-pill">C (Basic)</span>
                        <span class="tag-pill">C++ (Basic)</span>
                        <span class="tag-pill">Java (Basic)</span>
                    </div>
                </div>
            </div>

        </div>
    </div>
</template>

<style scoped>
/* ══════════════════════════════════════════════════════
   MY SKILLS — PREMIUM REDESIGN
   Bento grid with glowing orbs, progress rings,
   glassmorphism, and staggered reveal animations
══════════════════════════════════════════════════════ */

/* ── Wrapper ── */
.skills--wrapper {
    padding: 80px 0 70px;
}

/* Heading reveal */
.skills--wrapper .heading--wrapper {
    opacity: 0;
    transform: translateY(-24px);
    transition: opacity 0.8s cubic-bezier(0.22, 1, 0.36, 1),
                transform 0.8s cubic-bezier(0.22, 1, 0.36, 1);
}
.active--s .heading--wrapper {
    opacity: 1;
    transform: translateY(0);
}

/* ══════════════════════════════════════════════════════
   BENTO GRID
══════════════════════════════════════════════════════ */
.sk-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-template-rows: auto auto;
    gap: 24px;
    margin-bottom: 70px;
}

/* Featured card spans full first row on desktop */
.sk-card--featured {
    grid-column: 1 / -1;
}

/* ══════════════════════════════════════════════════════
   SKILL CARD — Base
══════════════════════════════════════════════════════ */
.sk-card {
    position: relative;
    overflow: hidden;
    border-radius: 24px;
    padding: 36px 32px;
    background: rgba(15, 14, 40, 0.55);
    border: 1px solid rgba(255, 255, 255, 0.06);
    backdrop-filter: blur(16px);
    -webkit-backdrop-filter: blur(16px);

    /* Reveal animation */
    opacity: 0;
    transform: translateY(48px) scale(0.97);
    transition:
        opacity     0.9s  cubic-bezier(0.22, 1, 0.36, 1),
        transform   0.9s  cubic-bezier(0.22, 1, 0.36, 1),
        border-color 0.35s ease,
        box-shadow   0.35s ease,
        background   0.35s ease;
}
.sk-card.sk-card--visible {
    opacity: 1;
    transform: translateY(0) scale(1);
}

/* Hover lift */
.sk-card.sk-card--visible:hover {
    border-color: rgba(108, 99, 255, 0.25);
    box-shadow:
        0 24px 60px rgba(0, 0, 0, 0.35),
        0 0 40px rgba(108, 99, 255, 0.07);
    background: rgba(18, 16, 50, 0.65);
    transform: translateY(-6px) scale(1);
}

/* Subtle top-edge gradient shimmer */
.sk-card::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 1px;
    background: linear-gradient(90deg,
        transparent 0%,
        rgba(108, 99, 255, 0.35) 25%,
        rgba(155, 89, 245, 0.4) 50%,
        rgba(108, 99, 255, 0.35) 75%,
        transparent 100%
    );
    opacity: 0;
    transition: opacity 0.5s ease;
}
.sk-card.sk-card--visible::before {
    opacity: 1;
}

/* ══════════════════════════════════════════════════════
   ICON ANCHOR — positions glow relative to icon
══════════════════════════════════════════════════════ */
.sk-icon-anchor {
    position: relative;
    display: inline-flex;
    align-items: center;
    justify-content: center;
}

/* ══════════════════════════════════════════════════════
   BACKGROUND GLOW ORBS — centered behind each icon
══════════════════════════════════════════════════════ */
.sk-glow {
    position: absolute;
    width: 160px;
    height: 160px;
    border-radius: 50%;
    filter: blur(70px);
    opacity: 0.2;
    pointer-events: none;
    z-index: 0;
    /* Center perfectly behind the icon */
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    transition: opacity 0.5s ease;
}
.sk-card:hover .sk-glow {
    opacity: 0.35;
}
.sk-glow--figma {
    background: #a78bfa;
}
.sk-glow--ps {
    background: #38bdf8;
}
.sk-glow--ai {
    background: #34d399;
}

/* ══════════════════════════════════════════════════════
   CARD INNER LAYOUTS
══════════════════════════════════════════════════════ */
.sk-card__inner {
    position: relative;
    z-index: 1;
    display: flex;
    align-items: center;
    gap: 40px;
}
.sk-card__inner--vertical {
    flex-direction: column;
    align-items: stretch;
    gap: 0;
}

.sk-card__left {
    flex: 1;
}
.sk-card__right {
    flex-shrink: 0;
}

/* Top row for smaller cards (icon + ring side by side) */
.sk-card__top-row {
    display: flex;
    align-items: center;
    justify-content: space-between;
    width: 100%;
    margin-bottom: 20px;
}

/* ══════════════════════════════════════════════════════
   ICON ORBS
══════════════════════════════════════════════════════ */
.sk-icon-orb {
    width: 56px;
    height: 56px;
    border-radius: 16px;
    display: flex;
    align-items: center;
    justify-content: center;
    position: relative;
    z-index: 1;
    transition: transform 0.3s ease, box-shadow 0.3s ease;
}
.sk-card:hover .sk-icon-orb {
    transform: scale(1.08);
}

/* Icon anchor in featured card left column needs bottom margin */
.sk-card__left > .sk-icon-anchor {
    margin-bottom: 20px;
}

.sk-icon-orb svg { width: 26px; height: 26px; }

/* Figma orb */
.sk-icon-orb--figma {
    background: rgba(167, 139, 250, 0.12);
    border: 1px solid rgba(167, 139, 250, 0.2);
    color: #a78bfa;
    box-shadow: 0 0 20px rgba(167, 139, 250, 0.15);
}
.sk-card:hover .sk-icon-orb--figma {
    box-shadow: 0 0 30px rgba(167, 139, 250, 0.3);
}

/* Photoshop orb */
.sk-icon-orb--ps {
    background: rgba(56, 189, 248, 0.1);
    border: 1px solid rgba(56, 189, 248, 0.2);
    color: #38bdf8;
    font-weight: 700;
    font-size: 19px;
    font-family: var(--font-body);
    box-shadow: 0 0 20px rgba(56, 189, 248, 0.12);
}
.sk-card:hover .sk-icon-orb--ps {
    box-shadow: 0 0 30px rgba(56, 189, 248, 0.25);
}

/* AI orb */
.sk-icon-orb--ai {
    background: rgba(52, 211, 153, 0.1);
    border: 1px solid rgba(52, 211, 153, 0.2);
    color: #34d399;
    box-shadow: 0 0 20px rgba(52, 211, 153, 0.12);
}
.sk-icon-orb--ai svg { width: 28px; height: 28px; }
.sk-card:hover .sk-icon-orb--ai {
    box-shadow: 0 0 30px rgba(52, 211, 153, 0.25);
}

/* ══════════════════════════════════════════════════════
   META: Title + Level Badge
══════════════════════════════════════════════════════ */
.sk-card__meta {
    display: flex;
    align-items: center;
    gap: 14px;
    margin-bottom: 12px;
}
.sk-card__title {
    font-family: var(--font-display);
    font-size: 24px;
    font-weight: 600;
    color: #fff;
    margin: 0;
    letter-spacing: 0.2px;
}
.sk-card__level {
    font-family: var(--font-body);
    font-size: 11px;
    font-weight: 500;
    text-transform: uppercase;
    letter-spacing: 1.2px;
    padding: 4px 14px;
    border-radius: 50px;
}
.sk-card__level--figma {
    color: #c4b5fd;
    background: rgba(167, 139, 250, 0.1);
    border: 1px solid rgba(167, 139, 250, 0.2);
}
.sk-card__level--ps {
    color: #7dd3fc;
    background: rgba(56, 189, 248, 0.1);
    border: 1px solid rgba(56, 189, 248, 0.18);
}
.sk-card__level--ai {
    color: #6ee7b7;
    background: rgba(52, 211, 153, 0.1);
    border: 1px solid rgba(52, 211, 153, 0.18);
}

/* Description */
.sk-card__desc {
    font-family: var(--font-body);
    font-size: 14.5px;
    line-height: 1.75;
    color: rgba(255, 255, 255, 0.5);
    margin: 0;
    max-width: 520px;
}

/* ══════════════════════════════════════════════════════
   PROGRESS RINGS (SVG)
══════════════════════════════════════════════════════ */
.sk-ring {
    position: relative;
    width: 110px;
    height: 110px;
}
.sk-ring--sm {
    width: 72px;
    height: 72px;
}
.sk-ring__svg {
    width: 100%;
    height: 100%;
    transform: rotate(-90deg);
}
.sk-ring__track {
    fill: none;
    stroke: rgba(255, 255, 255, 0.06);
    stroke-width: 7;
}
.sk-ring__fill {
    fill: none;
    stroke-width: 7;
    stroke-linecap: round;
    stroke-dasharray: 326.7;
    stroke-dashoffset: 326.7;
    transition: stroke-dashoffset 1.8s cubic-bezier(0.22, 1, 0.36, 1);
}
.sk-ring__fill--figma {
    stroke: url(#grad-figma);
    stroke: #a78bfa;
    filter: drop-shadow(0 0 6px rgba(167, 139, 250, 0.4));
}
.sk-ring__fill--ps {
    stroke: #38bdf8;
    filter: drop-shadow(0 0 6px rgba(56, 189, 248, 0.35));
}
.sk-ring__fill--ai {
    stroke: #34d399;
    filter: drop-shadow(0 0 6px rgba(52, 211, 153, 0.35));
}

.sk-ring__value {
    position: absolute;
    inset: 0;
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: var(--font-display);
    font-size: 28px;
    font-weight: 700;
    color: #fff;
    letter-spacing: -0.5px;
}
.sk-ring__value small {
    font-size: 14px;
    font-weight: 500;
    opacity: 0.5;
    margin-left: 1px;
}
.sk-ring__value--sm {
    font-size: 18px;
}
.sk-ring__value--sm small {
    font-size: 10px;
}

/* ══════════════════════════════════════════════════════
   AI TOOLS TAGS
══════════════════════════════════════════════════════ */
.sk-tools {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
    margin-top: 16px;
}
.sk-tool {
    font-family: var(--font-body);
    font-size: 12px;
    font-weight: 400;
    color: rgba(255, 255, 255, 0.7);
    background: rgba(52, 211, 153, 0.06);
    border: 1px solid rgba(52, 211, 153, 0.15);
    border-radius: 50px;
    padding: 4px 14px;
    transition: background 0.25s ease, border-color 0.25s ease, color 0.25s ease;
}
.sk-tool:hover {
    background: rgba(52, 211, 153, 0.14);
    border-color: rgba(52, 211, 153, 0.3);
    color: #6ee7b7;
}

/* ══════════════════════════════════════════════════════
   ADDITIONAL SKILLS
══════════════════════════════════════════════════════ */
.sk-extra {
    text-align: center;
    margin-top: 20px;
}
.sk-extra__title {
    font-family: var(--font-display);
    font-size: 24px;
    font-weight: 600;
    color: #ffffff;
    margin-bottom: 40px;
    opacity: 0;
    transform: translateY(20px);
    transition: opacity 0.7s 0.1s ease, transform 0.7s 0.1s ease;
}
.active--s .sk-extra__title {
    opacity: 1;
    transform: translateY(0);
}

.sk-category {
    margin-bottom: 32px;
}
.sk-category__label {
    font-family: var(--font-body);
    font-size: 13px;
    font-weight: 500;
    text-transform: uppercase;
    letter-spacing: 2px;
    color: rgba(108, 99, 255, 0.8);
    margin-bottom: 18px;
}

.sk-tags {
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    justify-content: center;
    gap: 10px;
    max-width: 900px;
    margin: 0 auto;
}

/* ── Tag Pills ── */
.tag-pill {
    font-family: var(--font-body);
    font-size: 13.5px;
    font-weight: 400;
    color: rgba(255, 255, 255, 0.8);
    background: rgba(255, 255, 255, 0.03);
    border: 1px solid rgba(255, 255, 255, 0.08);
    border-radius: 50px;
    padding: 8px 22px;
    cursor: default;
    user-select: none;

    /* Reveal animation */
    opacity: 0;
    transform: scale(0.88) translateY(12px);
    transition:
        opacity      0.55s cubic-bezier(0.22, 1, 0.36, 1),
        transform    0.55s cubic-bezier(0.34, 1.56, 0.64, 1),
        border-color 0.25s ease,
        background   0.25s ease,
        color        0.25s ease,
        box-shadow   0.25s ease;
}
.tag-pill.pill--visible {
    opacity: 1;
    transform: scale(1) translateY(0);
}
.tag-pill.pill--visible:hover {
    transform: scale(1.03) translateY(-3px);
    border-color: rgba(108, 99, 255, 0.45);
    background: rgba(108, 99, 255, 0.1);
    color: #ffffff;
    box-shadow: 0 6px 20px rgba(108, 99, 255, 0.15);
}

/* ══════════════════════════════════════════════════════
   RESPONSIVE
══════════════════════════════════════════════════════ */
@media screen and (max-width: 768px) {
    .sk-grid {
        grid-template-columns: 1fr;
    }

    /* On mobile, position Figma ring at top-right to match PS & AI cards */
    .sk-card--featured .sk-card__inner {
        flex-direction: column;
        align-items: flex-start;
        gap: 0;
    }
    .sk-card--featured .sk-card__right {
        position: absolute;
        top: 0;
        right: 0;
    }
    .sk-card--featured .sk-ring {
        width: 72px;
        height: 72px;
    }
    .sk-card--featured .sk-ring__value {
        font-size: 18px;
    }
    .sk-card--featured .sk-ring__value small {
        font-size: 10px;
    }

    .sk-card {
        padding: 28px 24px;
    }
    .sk-tags { gap: 8px; }
    .tag-pill { font-size: 13px; padding: 6px 16px; }
}

@media screen and (max-width: 450px) {
    .sk-card {
        padding: 24px 20px;
        border-radius: 18px;
    }
    .sk-card__title { font-size: 20px; }
    .sk-card__desc { font-size: 13.5px; }
    .sk-ring--sm,
    .sk-card--featured .sk-ring {
        width: 60px;
        height: 60px;
    }
    .sk-ring__value--sm,
    .sk-card--featured .sk-ring__value {
        font-size: 15px;
    }
    .sk-card--featured .sk-card__right {
        top: 0;
        right: 0;
    }
}
</style>