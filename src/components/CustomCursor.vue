<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

const isHovered = ref(false);
const isVisible = ref(false);

const cursorRef = ref(null);
const glowRef = ref(null);

let mouseX = -300;
let mouseY = -300;
let glowX = -300;
let glowY = -300;
let animFrameId = null;

const onMouseMove = (e) => {
    mouseX = e.clientX;
    mouseY = e.clientY;

    if (!isVisible.value) isVisible.value = true;

    // Instant 0-latency update for cursor tip
    if (cursorRef.value) {
        cursorRef.value.style.transform = `translate3d(${mouseX}px, ${mouseY}px, 0)`;
    }

    const target = e.target;
    if (target) {
        const isInteractive = target.closest('a, button, input, textarea, select, .project-card, .metric-card, .philosophy-card, .social-icon, .detail-item, [role="button"]');
        isHovered.value = !!isInteractive;
    }
};

const onMouseLeave = () => {
    isVisible.value = false;
};

// Fast and snappy lerp loop for the glow follower
const loop = () => {
    glowX += (mouseX - glowX) * 0.45;
    glowY += (mouseY - glowY) * 0.45;

    if (glowRef.value) {
        glowRef.value.style.transform = `translate3d(${glowX - 130}px, ${glowY - 130}px, 0)`;
    }

    animFrameId = requestAnimationFrame(loop);
};

onMounted(() => {
    window.addEventListener('mousemove', onMouseMove, { passive: true });
    document.addEventListener('mouseleave', onMouseLeave);
    loop();
});

onUnmounted(() => {
    window.removeEventListener('mousemove', onMouseMove, { passive: true });
    document.removeEventListener('mouseleave', onMouseLeave);
    if (animFrameId) cancelAnimationFrame(animFrameId);
});
</script>

<template>
    <div class="cursor-container" :class="{ 'is-active': isVisible }">

        <!-- 1. Ambient Blurred Purple Glow Circle -->
        <div ref="glowRef" class="glow-follower"></div>

        <!-- 2. Figma-style Designer Cursor Arrow -->
        <div ref="cursorRef" class="designer-cursor" :class="{ 'cursor-hover': isHovered }">
            <svg class="cursor-svg arrow-icon" width="24" height="26" viewBox="0 0 24 26" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path
                    d="M2.5 2L10.5 22.5L14.2 13.5L22.5 9.8L2.5 2Z"
                    fill="url(#cursor-gradient)"
                    stroke="#FFFFFF"
                    stroke-width="1.8"
                    stroke-linejoin="round"
                />
                <defs>
                    <linearGradient id="cursor-gradient" x1="2.5" y1="2" x2="22.5" y2="22.5" gradientUnits="userSpaceOnUse">
                        <stop stop-color="#6C63FF" />
                        <stop offset="1" stop-color="#9B59F5" />
                    </linearGradient>
                </defs>
            </svg>
        </div>

    </div>
</template>

<style>
/* Hide default cursor on desktop devices with fine pointer globally */
@media (pointer: fine) {
    * {
        cursor: none !important;
    }
}
</style>

<style scoped>
.cursor-container {
    pointer-events: none;
    position: fixed;
    inset: 0;
    z-index: 999999;
    opacity: 0;
    transition: opacity 0.4s ease;
}

.cursor-container.is-active {
    opacity: 1;
}

/* ── Ambient Blurred Purple Glow Circle ── */
.glow-follower {
    position: fixed;
    top: 0;
    left: 0;
    width: 240px;
    height: 240px;
    border-radius: 50%;
    background: radial-gradient(
        circle,
        rgba(155, 89, 245, 0.18) 0%,
        rgba(108, 99, 255, 0.09) 45%,
        rgba(108, 99, 255, 0.02) 65%,
        transparent 80%
    );
    filter: blur(36px);
    opacity: 0.65;
    z-index: 0;
    pointer-events: none;
    will-change: transform;
}

/* ── 2. Designer Cursor Arrow ── */
.designer-cursor {
    position: fixed;
    top: 0;
    left: 0;
    pointer-events: none;
    will-change: transform;
    display: flex;
    align-items: center;
    gap: 6px;
}

.cursor-svg {
    filter: drop-shadow(0 4px 10px rgba(108, 99, 255, 0.5));
    transition: transform 0.2s cubic-bezier(0.22, 1, 0.36, 1);
}

.designer-cursor.cursor-hover .cursor-svg {
    transform: scale(1.22) rotate(-8deg);
}

/* Figma-like designer badge tag */
.cursor-tag {
    font-size: 10px;
    font-family: var(--font-body);
    font-weight: 600;
    color: #ffffff;
    background: linear-gradient(90deg, #6c63ff 0%, #9b59f5 100%);
    padding: 2px 8px;
    border-radius: 50px;
    box-shadow: 0 4px 12px rgba(108, 99, 255, 0.4);
    letter-spacing: 0.5px;
    text-transform: uppercase;
    animation: tag-pop 0.2s cubic-bezier(0.22, 1, 0.36, 1);
    white-space: nowrap;
}

@keyframes tag-pop {
    0%   { opacity: 0; transform: scale(0.7); }
    100% { opacity: 1; transform: scale(1); }
}

@media (pointer: coarse) {
    .cursor-container {
        display: none !important;
    }
}
</style>
