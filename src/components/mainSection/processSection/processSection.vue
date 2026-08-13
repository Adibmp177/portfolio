<script setup>
import { ref, onMounted, onUnmounted, computed } from 'vue';

const activeStep = ref(0);
const panelRef = ref(null);
const isMobile = ref(false);

const checkMobile = () => {
    if (typeof window !== 'undefined') {
        isMobile.value = window.innerWidth <= 768;
    }
};

const steps = [
    {
        number: "01",
        label: "Discover",
        icon: `<svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" d="m21 21-5.197-5.197m0 0A7.5 7.5 0 1 0 5.196 5.196a7.5 7.5 0 0 0 10.607 10.607Z" /></svg>`,
        title: "Discovery & Research",
        subtitle: "Understanding before designing",
        description: "I immerse myself in your goals, audience, and market to build a foundation of insight before any design begins.",
        outcomes: ["User personas & empathy maps", "Competitive analysis", "Problem definition", "Project scope & metrics"],
        color: "#6c63ff",
        colorRgb: "108, 99, 255",
        duration: "1–2 days"
    },
    {
        number: "02",
        label: "Define",
        icon: `<svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" d="M9 12h3.75M9 15h3.75M9 18h3.75m3 .75H18a2.25 2.25 0 0 0 2.25-2.25V6.108c0-1.135-.845-2.098-1.976-2.192a48.424 48.424 0 0 0-1.123-.08m-5.801 0c-.065.21-.1.433-.1.664 0 .414.336.75.75.75h4.5a.75.75 0 0 0 .75-.75 2.25 2.25 0 0 0-.1-.664m-5.8 0A2.251 2.251 0 0 1 13.5 2.25H15c1.012 0 1.867.668 2.15 1.586m-5.8 0c-.376.023-.75.05-1.124.08C9.095 4.01 8.25 4.973 8.25 6.108V8.25m0 0H4.875c-.621 0-1.125.504-1.125 1.125v11.25c0 .621.504 1.125 1.125 1.125h9.75c.621 0 1.125-.504 1.125-1.125V9.375c0-.621-.504-1.125-1.125-1.125H8.25ZM6.75 12h.008v.008H6.75V12Zm0 3h.008v.008H6.75V15Zm0 3h.008v.008H6.75V18Z" /></svg>`,
        title: "Define & Plan",
        subtitle: "Turning insights into a blueprint",
        description: "Research transforms into a clear roadmap — user flows, information architecture, and structure before any visuals.",
        outcomes: ["User journey maps", "Information architecture", "Content hierarchy", "Wireframe sketches"],
        color: "#9b59f5",
        colorRgb: "155, 89, 245",
        duration: "1–2 days"
    },
    {
        number: "03",
        label: "Design",
        icon: `<svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" d="M9.53 16.122a3 3 0 0 0-5.78 1.128 2.25 2.25 0 0 1-2.4 2.245 4.5 4.5 0 0 0 8.4-2.245c0-.399-.078-.78-.22-1.128Zm0 0a15.998 15.998 0 0 0 3.388-1.62m-5.043-.025a15.994 15.994 0 0 1 1.622-3.395m3.42 3.42a15.995 15.995 0 0 0 4.764-4.648l3.876-5.814a1.151 1.151 0 0 0-1.597-1.597L14.146 6.32a15.996 15.996 0 0 0-4.649 4.763m3.42 3.42a6.776 6.776 0 0 0-3.42-3.42" /></svg>`,
        title: "Design & Iterate",
        subtitle: "Bringing ideas to high-fidelity life",
        description: "Pixel-perfect UI screens crafted in Figma with a consistent design system, reusable components, and interactive prototypes.",
        outcomes: ["High-fidelity UI screens", "Design system & tokens", "Interactive prototype", "Responsive layouts"],
        color: "#c94b96",
        colorRgb: "201, 75, 150",
        duration: "5–14 days"
    },
    {
        number: "04",
        label: "Test",
        icon: `<svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" d="M9 12.75 11.25 15 15 9.75M21 12c0 1.268-.63 2.39-1.593 3.068a3.745 3.745 0 0 1-1.043 3.296 3.745 3.745 0 0 1-3.296 1.043A3.745 3.745 0 0 1 12 21c-1.268 0-2.39-.63-3.068-1.593a3.746 3.746 0 0 1-3.296-1.043 3.745 3.745 0 0 1-1.043-3.296A3.745 3.745 0 0 1 12 3c1.268 0 2.39.63 3.068 1.593a3.746 3.746 0 0 1 3.296 1.043 3.746 3.746 0 0 1 1.043 3.296A3.746 3.746 0 0 1 1.043 3.296A3.745 3.745 0 0 1 21 12Z" /></svg>`,
        title: "Test & Validate",
        subtitle: "Real users, real feedback",
        description: "Designs are pressure-tested through usability sessions and feedback loops — refining until the experience feels effortless.",
        outcomes: ["Usability testing", "Heuristic evaluation", "A/B test insights", "Design refinements"],
        color: "#f59e0b",
        colorRgb: "245, 158, 11",
        duration: "2–4 days"
    },
    {
        number: "05",
        label: "Deliver",
        icon: `<svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" d="M15.59 14.37a6 6 0 0 1-5.84 7.38v-4.8m5.84-2.58a14.98 14.98 0 0 0 6.16-12.12A14.98 14.98 0 0 0 9.631 8.41m5.96 5.96a14.926 14.926 0 0 1-5.841 2.58m-.119-8.54a6 6 0 0 0-7.381 5.84h4.8m2.581-5.84a14.927 14.927 0 0 0-2.58 5.84m2.699 2.7c-.103.021-.207.041-.311.06a15.09 15.09 0 0 1-2.448-2.448 14.9 14.9 0 0 1 .06-.312m-2.24 2.39a4.493 4.493 0 0 0-1.757 4.306 4.493 4.493 0 0 0 4.306-1.758M16.5 9a1.5 1.5 0 1 1-3 0 1.5 1.5 0 0 1 3 0Z" /></svg>`,
        title: "Deliver & Support",
        subtitle: "Handoff that developers love",
        description: "Organized Figma files with annotated specs and assets — plus ongoing support throughout the development phase.",
        outcomes: ["Developer-ready files", "Design tokens & assets", "Annotated specs", "Implementation support"],
        color: "#34d399",
        colorRgb: "52, 211, 153",
        duration: "1–2 days"
    }
];

// Touch Drag state
const touchStartX = ref(0);
const touchStartY = ref(0);
const dragOffsetX = ref(0);
const isDragging = ref(false);

// Calculate exact real-time position including finger drag
const currentStepPosition = computed(() => {
    const viewportWidth = panelRef.value?.offsetWidth || 360;
    const dragFraction = -dragOffsetX.value / viewportWidth;
    const val = activeStep.value + dragFraction;
    return Math.max(0, Math.min(steps.length - 1, val));
});

// Real-time smooth progress line width on the timeline
const progressLineWidth = computed(() => {
    return (currentStepPosition.value / (steps.length - 1)) * 100 + '%';
});

// Live active node index based on touch drag
const liveActiveIndex = computed(() => {
    return Math.round(currentStepPosition.value);
});

function goToStep(index) {
    activeStep.value = index;
}
function prevStep() {
    if (activeStep.value > 0) activeStep.value--;
}
function nextStep() {
    if (activeStep.value < steps.length - 1) activeStep.value++;
}

function handleTouchStart(e) {
    touchStartX.value = e.touches[0].clientX;
    touchStartY.value = e.touches[0].clientY;
    dragOffsetX.value = 0;
}

function handleTouchMove(e) {
    if (!touchStartX.value) return;
    const currentX = e.touches[0].clientX;
    const currentY = e.touches[0].clientY;
    const diffX = currentX - touchStartX.value;
    const diffY = currentY - touchStartY.value;

    if (Math.abs(diffX) > Math.abs(diffY)) {
        isDragging.value = true;
        // Rubber-band resistance at track boundaries
        if ((activeStep.value === 0 && diffX > 0) || (activeStep.value === steps.length - 1 && diffX < 0)) {
            dragOffsetX.value = diffX * 0.25;
        } else {
            dragOffsetX.value = diffX;
        }
    }
}

function handleTouchEnd() {
    if (!isDragging.value) return;
    const threshold = 55;

    if (dragOffsetX.value < -threshold && activeStep.value < steps.length - 1) {
        nextStep();
    } else if (dragOffsetX.value > threshold && activeStep.value > 0) {
        prevStep();
    }

    isDragging.value = false;
    dragOffsetX.value = 0;
    touchStartX.value = 0;
    touchStartY.value = 0;
}

onMounted(() => {
    checkMobile();
    if (typeof window !== 'undefined') {
        window.addEventListener('resize', checkMobile);
    }

    const Observer = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
            if (entry.isIntersecting) {
                entry.target.classList.add('active--s');
                Observer.unobserve(entry.target);
            }
        });
    }, {
        rootMargin: '-10% 0px -10% 0px'
    });

    const wrapper = document.querySelector('.process--wrapper');
    if (wrapper) Observer.observe(wrapper);
});

onUnmounted(() => {
    if (typeof window !== 'undefined') {
        window.removeEventListener('resize', checkMobile);
    }
});
</script>

<template>
    <div class="process--wrapper">
        <div class="container">

            <!-- Section Heading -->
            <div class="heading--wrapper">
                <h2 class="heading">My Design Process</h2>
            </div>

            <!-- Timeline Navigation (Line and nodes update live during touch drag) -->
            <div class="timeline-nav">
                <div class="timeline-track">
                    <div class="timeline-track-fill" :style="{ width: progressLineWidth }"></div>
                </div>
                <div
                    v-for="(step, index) in steps"
                    :key="index"
                    class="timeline-node"
                    :class="{ 'is-active': liveActiveIndex === index, 'is-done': index < liveActiveIndex }"
                    @click="goToStep(index)"
                    :style="`--node-accent: ${step.color}; --node-rgb: ${step.colorRgb};`"
                >
                    <div class="node-circle">
                        <span class="node-num">{{ step.number }}</span>
                    </div>
                    <span class="node-label">{{ step.label }}</span>
                </div>
            </div>

            <!-- Outer Viewport for the 5 Distinct Boxes Carousel -->
            <div
                ref="panelRef"
                class="process-carousel-viewport"
                @touchstart="handleTouchStart"
                @touchmove="handleTouchMove"
                @touchend="handleTouchEnd"
            >
                <!-- Horizontal Track moving 5 distinct boxes -->
                <div
                    class="carousel-track"
                    :style="{
                        transform: isMobile
                            ? `translateX(calc(-${activeStep * 100}% + ${dragOffsetX}px))`
                            : `translateX(calc(-${activeStep * 100}% - ${activeStep * 24}px + ${dragOffsetX}px))`,
                        transition: isDragging ? 'none' : 'transform 0.45s cubic-bezier(0.22, 1, 0.36, 1)'
                    }"
                >
                    <!-- 5 Completely Independent, Distinct Step Cards/Boxes -->
                    <div
                        v-for="(step, index) in steps"
                        :key="index"
                        class="single-step-card"
                        :style="`--panel-accent: ${step.color}; --panel-rgb: ${step.colorRgb};`"
                    >
                        <div class="step-panel-box">
                            <!-- Custom Ambient Glow Blob inside THIS box -->
                            <div class="card-glow-blob"></div>

                            <div class="panel-body">
                                <!-- Left: Icon + Meta -->
                                <div class="panel-left">
                                    <div class="step-icon-wrap">
                                        <div class="step-icon" v-html="step.icon"></div>
                                        <div class="step-glow"></div>
                                    </div>
                                    <div class="step-meta">
                                        <span class="step-number-badge">{{ step.number }}</span>
                                        <div class="step-duration">
                                            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" d="M12 6v6h4.5m4.5 0a9 9 0 1 1-18 0 9 9 0 0 1 18 0Z" /></svg>
                                            <span>{{ step.duration }}</span>
                                        </div>
                                    </div>
                                </div>

                                <!-- Right: Content -->
                                <div class="panel-right">
                                    <div class="step-header">
                                        <h3 class="step-title">{{ step.title }}</h3>
                                        <p class="step-subtitle">{{ step.subtitle }}</p>
                                    </div>
                                    <p class="step-description">{{ step.description }}</p>

                                    <div class="outcomes-section">
                                        <p class="outcomes-label">Key Outcomes</p>
                                        <ul class="outcomes-list">
                                            <li
                                                v-for="(outcome, i) in step.outcomes"
                                                :key="i"
                                                class="outcome-item"
                                            >
                                                <span class="outcome-check">
                                                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="2.5" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" d="m4.5 12.75 6 6 9-13.5" /></svg>
                                                </span>
                                                {{ outcome }}
                                            </li>
                                        </ul>
                                    </div>
                                </div>
                            </div>

                            <!-- Bottom Navigation Bar inside THIS distinct box -->
                            <div class="panel-nav-bar">
                                <button
                                    class="nav-btn"
                                    :class="{ 'nav-btn--disabled': index === 0 }"
                                    :disabled="index === 0"
                                    @click.stop="prevStep"
                                    aria-label="Previous step"
                                >
                                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" d="M15.75 19.5 8.25 12l7.5-7.5" /></svg>
                                    <span>Previous Step</span>
                                </button>

                                <div class="nav-step-indicator">
                                    <div
                                        v-for="(_, i) in steps"
                                        :key="i"
                                        class="indicator-pip"
                                        :class="{ 'pip-active': i === index, 'pip-done': i < index }"
                                        @click.stop="goToStep(i)"
                                    ></div>
                                </div>

                                <button
                                    class="nav-btn nav-btn--next"
                                    :class="{ 'nav-btn--disabled': index === steps.length - 1 }"
                                    :disabled="index === steps.length - 1"
                                    @click.stop="nextStep"
                                    aria-label="Next step"
                                >
                                    <span>Next Step</span>
                                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" d="m8.25 4.5 7.5 7.5-7.5 7.5" /></svg>
                                </button>
                            </div>

                        </div>
                    </div>
                </div>
            </div>

        </div>
    </div>
</template>

<style scoped>
/* ── Wrapper ── */
.process--wrapper {
    padding: 90px 0 100px;
    position: relative;
}

/* ── Section Heading ── */
.process--wrapper .heading--wrapper {
    opacity: 0;
    transform: translateY(-24px);
    transition: opacity 0.8s cubic-bezier(0.22, 1, 0.36, 1), transform 0.8s cubic-bezier(0.22, 1, 0.36, 1);
    margin-bottom: 60px;
}
.active--s .heading--wrapper {
    opacity: 1;
    transform: translateY(0);
}

/* ═══════════════════════════════════════
   TIMELINE NAV
═══════════════════════════════════════ */
.timeline-nav {
    position: relative;
    display: flex;
    align-items: flex-start;
    justify-content: space-between;
    margin-bottom: 48px;
    padding: 0 10px;
    opacity: 0;
    transform: translateY(20px);
    transition: opacity 0.8s 0.15s cubic-bezier(0.22, 1, 0.36, 1), transform 0.8s 0.15s cubic-bezier(0.22, 1, 0.36, 1);
}
.active--s .timeline-nav {
    opacity: 1;
    transform: translateY(0);
}

/* Connecting track line */
.timeline-track {
    position: absolute;
    top: 23px;
    left: 10%;
    right: 10%;
    height: 3px;
    background: rgba(255, 255, 255, 0.08);
    border-radius: 3px;
    overflow: hidden;
    z-index: 1;
}
.timeline-track-fill {
    height: 100%;
    background: linear-gradient(90deg, #6c63ff 0%, #9b59f5 40%, #c94b96 70%, #f59e0b 90%, #34d399 100%);
    border-radius: 3px;
    transition: width 0.1s linear;
}

/* Individual step node */
.timeline-node {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 10px;
    cursor: pointer;
    flex: 1;
    position: relative;
    z-index: 5;
    opacity: 1;
}

.node-circle {
    width: 46px;
    height: 46px;
    border-radius: 50%;
    background: #090b1c;
    border: 2px solid rgba(255, 255, 255, 0.15);
    display: flex;
    align-items: center;
    justify-content: center;
    transition: all 0.35s cubic-bezier(0.22, 1, 0.36, 1);
    box-shadow: 0 4px 14px rgba(0, 0, 0, 0.6);
}
.node-num {
    font-family: var(--font-display);
    font-size: 13px;
    font-weight: 700;
    color: rgba(255, 255, 255, 0.45);
    transition: color 0.3s ease;
    letter-spacing: 0.3px;
}
.node-label {
    font-size: 12px;
    color: rgba(255, 255, 255, 0.4);
    font-weight: 500;
    letter-spacing: 0.3px;
    transition: color 0.3s ease;
}

/* Completed steps */
.timeline-node.is-done .node-circle {
    border: 2px solid var(--node-accent);
    background: #090b1c;
    box-shadow: 0 0 14px rgba(var(--node-rgb), 0.35);
}
.timeline-node.is-done .node-num {
    color: #ffffff;
}
.timeline-node.is-done .node-label {
    color: rgba(255, 255, 255, 0.85);
}

/* Active step */
.timeline-node.is-active .node-circle {
    background: #090b1c;
    border: 2.5px solid var(--node-accent);
    box-shadow: 0 0 0 4px rgba(var(--node-rgb), 0.15), 0 0 20px rgba(var(--node-rgb), 0.5);
    transform: scale(1.14);
}
.timeline-node.is-active .node-num {
    color: #ffffff;
}
.timeline-node.is-active .node-label {
    color: #ffffff;
    font-weight: 600;
}

/* Hover for inactive nodes */
.timeline-node:not(.is-active):hover .node-circle {
    border-color: rgba(255, 255, 255, 0.35);
    transform: scale(1.06);
}
.timeline-node:not(.is-active):hover .node-label {
    color: rgba(255, 255, 255, 0.7);
}

/* ═══════════════════════════════════════
   CAROUSEL VIEWPORT & 5 DISTINCT BOXES TRACK
═══════════════════════════════════════ */
.process-carousel-viewport {
    overflow: hidden;
    width: 100%;
    position: relative;
    touch-action: pan-y;
    user-select: none;
    padding: 12px 0 24px;
    margin: -12px 0 -24px;
}

.carousel-track {
    display: flex;
    gap: 24px;
    width: 100%;
    position: relative;
    will-change: transform;
}

.single-step-card {
    flex: 0 0 100%;
    width: 100%;
    min-width: 100%;
}

/* EACH INDIVIDUAL DISTINCT BOX (With its own border, background, shadow, glow, and nav bar) */
.step-panel-box {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    height: 390px;
    background: linear-gradient(145deg, rgba(14, 13, 36, 0.94) 0%, rgba(10, 9, 28, 0.98) 100%);
    border: 1px solid rgba(var(--panel-rgb), 0.25);
    border-radius: 24px;
    padding: 34px 44px 0;
    backdrop-filter: blur(20px);
    box-shadow:
        0 24px 60px rgba(0, 0, 0, 0.55),
        0 0 0 1px rgba(255, 255, 255, 0.04),
        0 0 50px rgba(var(--panel-rgb), 0.08),
        inset 0 1px 0 rgba(255, 255, 255, 0.07);
    position: relative;
    overflow: hidden;
    transition: border-color 0.45s ease, box-shadow 0.45s ease;
}

/* Custom Glow Blob for THIS box */
.card-glow-blob {
    position: absolute;
    top: -110px; right: -110px;
    width: 380px; height: 380px;
    border-radius: 50%;
    background: radial-gradient(circle, rgba(var(--panel-rgb), 0.16) 0%, rgba(var(--panel-rgb), 0.04) 50%, transparent 70%);
    pointer-events: none;
    transition: background 0.5s ease;
}

.panel-body {
    display: flex;
    gap: 36px;
    flex: 1;
    min-height: 0;
    position: relative;
    z-index: 1;
}

/* ── Panel Left ── */
.panel-left {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 20px;
    flex-shrink: 0;
    width: 130px;
}

.step-icon-wrap {
    position: relative;
    display: flex;
    align-items: center;
    justify-content: center;
}
.step-icon {
    width: 68px;
    height: 68px;
    background: linear-gradient(145deg, rgba(var(--panel-rgb), 0.14) 0%, rgba(var(--panel-rgb), 0.05) 100%);
    border: 1.5px solid rgba(var(--panel-rgb), 0.4);
    border-radius: 20px;
    display: flex;
    align-items: center;
    justify-content: center;
    color: var(--panel-accent);
    position: relative;
    z-index: 1;
    box-shadow: 0 8px 24px rgba(var(--panel-rgb), 0.15), inset 0 1px 0 rgba(255, 255, 255, 0.08);
}
.step-icon :deep(svg) {
    width: 30px;
    height: 30px;
}
.step-glow {
    position: absolute;
    width: 85px;
    height: 85px;
    border-radius: 50%;
    background: radial-gradient(circle, rgba(var(--panel-rgb), 0.3) 0%, transparent 70%);
    pointer-events: none;
    filter: blur(10px);
    animation: glow-pulse 3s ease-in-out infinite;
}
@keyframes glow-pulse {
    0%, 100% { opacity: 0.4; transform: scale(1); }
    50% { opacity: 0.8; transform: scale(1.15); }
}

.step-meta {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 10px;
}
.step-number-badge {
    font-family: var(--font-display);
    font-size: 34px;
    font-weight: 700;
    color: rgba(var(--panel-rgb), 0.4);
    line-height: 1;
    letter-spacing: -1px;
}
.step-duration {
    display: flex;
    align-items: center;
    gap: 5px;
    font-size: 12px;
    color: rgba(255, 255, 255, 0.55);
    background: rgba(255, 255, 255, 0.04);
    border: 1px solid rgba(255, 255, 255, 0.08);
    border-radius: 50px;
    padding: 5px 12px;
    white-space: nowrap;
}
.step-duration svg {
    width: 13px;
    height: 13px;
    flex-shrink: 0;
}

/* ── Panel Right ── */
.panel-right {
    flex: 1;
    min-width: 0;
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
}

.step-header {
    margin-bottom: 10px;
}
.step-title {
    font-family: var(--font-display);
    font-size: clamp(22px, 2.5vw, 27px);
    font-weight: 700;
    color: #fff;
    margin: 0 0 4px;
    line-height: 1.2;
}
.step-subtitle {
    font-size: 14px;
    color: var(--panel-accent);
    font-weight: 500;
    margin: 0;
    letter-spacing: 0.2px;
}

.step-description {
    font-size: 14.5px;
    color: rgba(255, 255, 255, 0.68);
    line-height: 1.65;
    margin: 0;
}

/* Outcomes */
.outcomes-section {
    margin-top: 30px;
    margin-bottom: 16px;
}
.outcomes-label {
    font-size: 11px;
    font-weight: 600;
    color: rgba(255, 255, 255, 0.45);
    text-transform: uppercase;
    letter-spacing: 1.2px;
    margin-bottom: 10px;
}
.outcomes-list {
    list-style: none;
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 8px 22px;
    padding: 0;
    margin: 0;
}
.outcome-item {
    display: flex;
    align-items: center;
    gap: 10px;
    font-size: 13.5px;
    color: rgba(255, 255, 255, 0.75);
}
.outcome-check {
    width: 20px;
    height: 20px;
    border-radius: 50%;
    background: rgba(var(--panel-rgb), 0.12);
    border: 1px solid rgba(var(--panel-rgb), 0.35);
    display: flex;
    align-items: center;
    justify-content: center;
    flex-shrink: 0;
    color: var(--panel-accent);
}
.outcome-check svg {
    width: 11px;
    height: 11px;
}

/* ═══════════════════════════════════════
   BOTTOM NAVIGATION BAR INSIDE THIS BOX
═══════════════════════════════════════ */
.panel-nav-bar {
    display: flex;
    align-items: center;
    justify-content: space-between;
    width: calc(100% + 88px);
    margin: 0 -44px;
    padding: 15px 44px;
    border-top: 1px solid rgba(255, 255, 255, 0.08);
    background: rgba(13, 11, 38, 0.4);
    position: relative;
    z-index: 1;
}

.nav-btn {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    padding: 11px 24px;
    background: rgba(255, 255, 255, 0.04);
    border: 1px solid rgba(255, 255, 255, 0.12);
    border-radius: 50px;
    color: rgba(255, 255, 255, 0.75);
    font-size: 14px;
    font-weight: 500;
    font-family: var(--font-body);
    cursor: pointer;
    transition: all 0.3s ease;
    user-select: none;
}
.nav-btn svg {
    width: 18px;
    height: 18px;
    flex-shrink: 0;
}
.nav-btn:not(.nav-btn--disabled):hover {
    background: rgba(255, 255, 255, 0.1);
    border-color: rgba(255, 255, 255, 0.3);
    color: #fff;
    transform: translateY(-2px);
}
.nav-btn:not(.nav-btn--disabled):active {
    transform: translateY(0) scale(0.97);
}

.nav-btn--next {
    background: linear-gradient(135deg, rgba(var(--panel-rgb), 0.35) 0%, rgba(var(--panel-rgb), 0.2) 100%);
    border: 1px solid rgba(var(--panel-rgb), 0.55);
    color: #ffffff;
    box-shadow: 0 4px 18px rgba(var(--panel-rgb), 0.2), inset 0 1px 0 rgba(255, 255, 255, 0.1);
    transition: all 0.3s ease;
}
.nav-btn--next:not(.nav-btn--disabled):hover {
    background: linear-gradient(135deg, rgba(var(--panel-rgb), 0.5) 0%, rgba(var(--panel-rgb), 0.3) 100%);
    border-color: var(--panel-accent);
    box-shadow: 0 8px 26px rgba(var(--panel-rgb), 0.35), inset 0 1px 0 rgba(255, 255, 255, 0.15);
    transform: translateY(-2px);
}

.nav-btn--disabled {
    opacity: 0.25;
    cursor: not-allowed;
    box-shadow: none !important;
}

/* Pip indicator in center */
.nav-step-indicator {
    display: flex;
    align-items: center;
    gap: 8px;
}
.indicator-pip {
    width: 8px;
    height: 8px;
    border-radius: 50%;
    background: rgba(255, 255, 255, 0.18);
    cursor: pointer;
    transition: all 0.3s ease;
}
.indicator-pip.pip-done {
    background: rgba(255, 255, 255, 0.4);
}
.indicator-pip.pip-active {
    background: var(--panel-accent);
    width: 24px;
    border-radius: 4px;
    box-shadow: 0 0 12px rgba(var(--panel-rgb), 0.5);
}
.indicator-pip:hover:not(.pip-active) {
    background: rgba(255, 255, 255, 0.35);
    transform: scale(1.2);
}

/* ═══════════════════════════════════════
   RESPONSIVE
═══════════════════════════════════════ */
@media screen and (max-width: 900px) {
    .step-panel-box {
        height: 500px;
        padding: 28px 26px 0;
    }
    .panel-body {
        flex-direction: column;
        gap: 16px;
    }
    .panel-left {
        flex-direction: row;
        width: 100%;
        gap: 18px;
        justify-content: flex-start;
    }
    .step-meta { flex-direction: row; align-items: center; gap: 14px; }
    .outcomes-section {
        margin-top: 16px;
        margin-bottom: 20px;
    }
    .panel-nav-bar {
        width: calc(100% + 52px);
        margin: 0 -26px;
        padding: 14px 26px;
    }
}

@media screen and (max-width: 768px) {
    /* Full bleed breakout on mobile so swipe goes edge-to-edge of phone screen */
    .process-carousel-viewport {
        width: 100vw;
        position: relative;
        left: 50%;
        right: 50%;
        margin-left: -50vw;
        margin-right: -50vw;
        padding: 12px 0 24px;
    }
    .carousel-track {
        gap: 0;
    }
    .single-step-card {
        flex: 0 0 100vw;
        width: 100vw;
        min-width: 100vw;
        box-sizing: border-box;
        padding: 0 20px;
    }
    .timeline-nav {
        overflow: visible;
        padding: 12px 0 8px;
        margin-bottom: 36px;
    }
    .timeline-track {
        display: block;
        top: 30px;
        left: 8%;
        right: 8%;
    }
    .node-circle {
        width: 38px;
        height: 38px;
    }
    .node-num {
        font-size: 12px;
    }
    .node-label {
        display: block;
        font-size: 11px;
        margin-top: 2px;
    }
    .outcomes-list { grid-template-columns: 1fr; }
    .nav-btn span { display: none; }
    .nav-btn { padding: 12px 16px; }
}

@media screen and (max-width: 480px) {
    .single-step-card {
        padding: 0 16px;
    }
    .step-panel-box {
        height: 510px;
        padding: 22px 18px 0;
    }
    .panel-left { flex-wrap: wrap; }
    .step-title { font-size: 20px; }
    .outcomes-section {
        margin-top: 14px;
        margin-bottom: 16px;
    }
    .panel-nav-bar {
        width: calc(100% + 36px);
        margin: 0 -18px;
        padding: 12px 18px;
    }
    .node-circle {
        width: 34px;
        height: 34px;
    }
    .node-num {
        font-size: 11px;
    }
    .node-label {
        font-size: 10px;
        letter-spacing: 0;
    }
    .timeline-track {
        top: 28px;
    }
}
</style>
