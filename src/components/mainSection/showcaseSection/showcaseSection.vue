<script setup>
import { ref, onMounted } from 'vue';

const projects = ref([
    {
        id: 1,
        title: "CineStream",
        year: "2026",
        description: "Website and app design for a Movie & TvShow Streaming Platform, with download option as secondary Action!",
        tags: ["Web Design", "App Design", "CaseStudy"],
        link: "https://www.figma.com/design/erH5Y0jXpNLxJAnPjSQraD/CineStream-CaseStudy?m=auto&t=vsksg6UYbGLPfKXZ-6",
        image: "CineStream.png"
    },
    {
        id: 2,
        title: "TakShop",
        year: "2025",
        description: "Website design for a digital gadget store, fully responsive with dark/light mode, user profile and shopping cart.",
        tags: ["Web Design", "App Design", "Dark/Light"],
        link: "https://www.figma.com/design/hlVbD1Q9JzGhYZ3iAA56bg/TakShop?m=auto&t=vsksg6UYbGLPfKXZ-7",
        image: "TakShop.png"
    },
    {
        id: 3,
        title: "Melodies",
        year: "2023",
        description: "Website design for a Music Streaming Platform, with playlist creation, artist pages, user profile, fully responsive.",
        tags: ["Web Design", "App Design"],
        link: "https://www.figma.com/design/tH8nINgjWQlFx6bxaSZvED/melodies-Web--final-?m=auto&t=vsksg6UYbGLPfKXZ-7",
        image: "Melodies.png"
    },
    {
        id: 4,
        title: "Prime Gaming",
        year: "2024",
        description: "Responsive landing page design for a Gaming platform, where users can buy & play games, read blogs, game reviews and ratings.",
        tags: ["Web Design", "App Design"],
        link: "https://www.figma.com/design/2wDuQFmBnqDrQWewwwjhM5/Gaming-Website?m=auto&t=vsksg6UYbGLPfKXZ-6",
        image: "PrimeGaming.png"
    },
    {
        id: 5,
        title: "Fitmaker",
        year: "2024",
        description: "Responsive landing page design for Fitmaker, a Fitness platform with blog, workout & nutrition programs, and trainer profiles.",
        tags: ["Web Design", "App Design"],
        link: "https://www.figma.com/design/3enOWXqLU3k0JLtxwmt6YC/FitMaker?m=auto&t=vsksg6UYbGLPfKXZ-6",
        image: "Fitmaker.png"
    },
    {
        id: 6,
        title: "Social Posts",
        year: "2023 - 2026",
        description: "Social media post designs for Instagram, focused on educational content to drive more engagement and reach.",
        tags: ["Post Design", "Custom Layout", "Branding"],
        link: "https://www.figma.com/design/Dw30tPvneV4NlyK62rpWn8/Social-Posts?m=auto&t=vsksg6UYbGLPfKXZ-6",
        image: "Social.png"
    }
]);

function getImageUrl(name) {
    if (!name) return '';
    try {
        return require(`@/assets/projectImages/${name}`);
    } catch (e) {
        return '';
    }
}

// ── Custom Mouse Follower Cursor ──
const isHovering = ref(false);
const cursorPos = ref({ x: 0, y: 0 });

function handleMouseMove(e) {
    cursorPos.value = { x: e.clientX, y: e.clientY };
}
function handleMouseEnter() {
    isHovering.value = true;
}
function handleMouseLeave() {
    isHovering.value = false;
}

onMounted(() => {
    const Observer = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
            if (entry.isIntersecting) {
                entry.target.classList.add('active--s');
                const cards = entry.target.querySelectorAll('.project-card');
                cards.forEach((card, i) => {
                    setTimeout(() => card.classList.add('card--visible'), i * 80);
                });
                Observer.unobserve(entry.target);
            }
        });
    }, {
        rootMargin: '-15% 0px -15% 0px'
    });

    let showcaseItems = document.querySelector('.showcase--wrapper');
    if (showcaseItems) Observer.observe(showcaseItems);
});
</script>

<template>
    <div class="showcase--wrapper">
        <div class="container">
            <div class="heading--wrapper">
                <h1 class="heading">Projects</h1>
            </div>

            <div class="projects-grid">
                <a 
                    v-for="p in projects" 
                    :key="p.id" 
                    :href="p.link" 
                    target="_blank" 
                    rel="noopener noreferrer" 
                    class="project-card"
                    @mousemove="handleMouseMove"
                    @mouseenter="handleMouseEnter"
                    @mouseleave="handleMouseLeave"
                >
                    <div class="p-image-container">
                        <img v-if="getImageUrl(p.image)" :src="getImageUrl(p.image)" :alt="p.title" class="p-image" />
                        <div v-else class="p-image-placeholder">
                            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="placeholder-icon">
                                <path stroke-linecap="round" stroke-linejoin="round" d="m2.25 15.75 5.159-5.159a2.25 2.25 0 0 1 3.182 0l5.159 5.159m-1.5-1.5 1.409-1.409a2.25 2.25 0 0 1 3.182 0l2.909 2.909m-18 3.75h16.5a1.5 1.5 0 0 0 1.5-1.5V6a1.5 1.5 0 0 0-1.5-1.5H3.75A1.5 1.5 0 0 0 2.25 6v12a1.5 1.5 0 0 0 1.5 1.5Zm10.5-11.25h.008v.008h-.008V8.25Zm.375 0a.375.375 0 1 1-.75 0 .375.375 0 0 1 .75 0Z" />
                            </svg>
                            <span>{{ p.title }} Preview</span>
                        </div>
                    </div>

                    <div class="p-content">
                        <div class="p-header">
                            <h3 class="p-title">{{ p.title }}</h3>
                            <span class="p-year">{{ p.year }}</span>
                        </div>

                        <p class="p-desc">{{ p.description }}</p>

                        <div class="p-footer">
                            <div class="p-tags">
                                <span v-for="t in p.tags" :key="t" class="p-tag">{{ t }}</span>
                            </div>

                            <div class="p-btn" aria-label="View Project in Figma">
                                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor">
                                    <path stroke-linecap="round" stroke-linejoin="round" d="M5 12h14m-7-7 7 7-7 7" />
                                </svg>
                            </div>
                        </div>
                    </div>
                </a>
            </div>

        </div>

        <!-- ── Floating "View in Figma" Mouse Cursor Tooltip ── -->
        <Teleport to="body">
            <div 
                class="figma-cursor-tooltip" 
                :class="{ 'is-active': isHovering }"
                :style="{ transform: `translate3d(${cursorPos.x + 14}px, ${cursorPos.y + 14}px, 0)` }"
            >
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 38 57" fill="currentColor" class="tooltip-figma-icon">
                    <path d="M19 28.5a9.5 9.5 0 1 1 19 0 9.5 9.5 0 0 1-19 0Z"/>
                    <path d="M0 47.5A9.5 9.5 0 0 1 9.5 38H19v9.5a9.5 9.5 0 0 1-19 0Z"/>
                    <path d="M19 0v19h9.5a9.5 9.5 0 0 0 0-19H19Z"/>
                    <path d="M0 9.5A9.5 9.5 0 0 0 9.5 19H19V0H9.5A9.5 9.5 0 0 0 0 9.5Z"/>
                    <path d="M0 28.5A9.5 9.5 0 0 0 9.5 38H19V19H9.5A9.5 9.5 0 0 0 0 28.5Z"/>
                </svg>
                <span>View in Figma</span>
            </div>
        </Teleport>
    </div>
</template>

<style scoped>
/* ── Wrapper & Scroll Animations ── */
.showcase--wrapper {
    padding: 70px 0;
}

/* Heading fades in with a slight slide-down */
.showcase--wrapper .heading--wrapper {
    opacity: 0;
    transform: translateY(-20px);
    transition: opacity 0.7s ease, transform 0.7s ease;
}
.active--s .heading--wrapper {
    opacity: 1;
    transform: translateY(0);
}

.projects-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(330px, 1fr));
    gap: 30px;
}

/* Each card starts hidden and slides up when .card--visible is added */
.project-card {
    background: rgba(18, 17, 43, 0.45);
    border: 1px solid rgba(255, 255, 255, 0.07);
    border-radius: 20px;
    overflow: hidden;
    display: flex;
    flex-direction: column;
    text-decoration: none;
    color: inherit;
    backdrop-filter: blur(8px);
    cursor: pointer;
    opacity: 0;
    transform: translateY(36px) scale(0.97);
    transition:
        opacity 0.6s cubic-bezier(0.22, 1, 0.36, 1),
        transform 0.6s cubic-bezier(0.22, 1, 0.36, 1),
        background 0.3s ease,
        border-color 0.3s ease,
        box-shadow 0.3s ease;
}
.project-card.card--visible {
    opacity: 1;
    transform: translateY(0) scale(1);
}
.project-card.card--visible:hover {
    transform: translateY(-6px) scale(1);
    background: rgba(22, 20, 52, 0.6);
    border-color: rgba(108, 99, 255, 0.35);
    box-shadow: 0 16px 40px rgba(0, 0, 0, 0.4), 0 0 20px rgba(108, 99, 255, 0.12);
}

.p-image-container {
    width: 100%;
    aspect-ratio: 16 / 9;
    position: relative;
    overflow: hidden;
    border-bottom: 1px solid rgba(255, 255, 255, 0.06);
    background: rgba(255, 255, 255, 0.03);
}

.p-image {
    width: 100%;
    height: 100%;
    object-fit: cover;
    object-position: center;
    transition: transform 0.4s ease;
}
.project-card:hover .p-image {
    transform: scale(1.05);
}

.p-image-placeholder {
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    color: rgba(108, 99, 255, 0.8);
    transition: background 0.3s ease;
}
.project-card:hover .p-image-placeholder {
    background: rgba(108, 99, 255, 0.06);
}

.placeholder-icon {
    width: 44px;
    height: 44px;
    margin-bottom: 8px;
    opacity: 0.6;
}
.p-image-placeholder span {
    font-size: 13px;
    color: rgba(255, 255, 255, 0.45);
}

.p-content {
    padding: 24px 22px 22px;
    display: flex;
    flex-direction: column;
    flex: 1;
}

.p-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 12px;
}
.p-title {
    font-family: var(--font-display);
    font-size: 21px;
    color: #ffffff;
    margin: 0;
    font-weight: 600;
}
.p-year {
    font-size: 13px;
    color: rgba(255, 255, 255, 0.45);
    background: transparent;
    border: none;
    padding: 0;
    font-weight: 500;
}

.p-desc {
    color: rgba(255, 255, 255, 0.65);
    font-size: 14px;
    line-height: 1.6;
    margin: 0 0 20px 0;
    overflow: hidden;
    display: -webkit-box;
    /* stylelint-disable-next-line */
    -webkit-box-orient: vertical;
    -webkit-line-clamp: 3;
    line-clamp: 3;
}

.p-footer {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-top: auto;
}

.p-tags {
    display: flex;
    align-items: center;
    flex-wrap: nowrap;
    gap: 6px;
    overflow-x: hidden;
}
.p-tag {
    font-size: 11px;
    color: rgba(255, 255, 255, 0.7);
    background: rgba(255, 255, 255, 0.04);
    padding: 3px 9px;
    border-radius: 50px;
    border: 1px solid rgba(255, 255, 255, 0.08);
    white-space: nowrap;
}

.p-btn {
    width: 38px;
    height: 38px;
    border-radius: 50%;
    background: rgba(255, 255, 255, 0.05);
    color: #fff;
    display: flex;
    align-items: center;
    justify-content: center;
    border: 1px solid rgba(255, 255, 255, 0.1);
    transition: background 0.3s ease, border-color 0.3s ease, box-shadow 0.3s ease, transform 0.3s ease;
    flex-shrink: 0;
}
.p-btn svg {
    width: 18px;
    height: 18px;
    transition: transform 0.3s ease;
}
.project-card:hover .p-btn {
    background: linear-gradient(90deg, #6c63ff 0%, #9b59f5 100%);
    border-color: transparent;
    box-shadow: 0 4px 15px rgba(108, 99, 255, 0.45);
}
.project-card:hover .p-btn svg {
    transform: rotate(-45deg);
}

/* ── Floating Tooltip ── */
.figma-cursor-tooltip {
    position: fixed;
    top: 0;
    left: 0;
    z-index: 99999;
    pointer-events: none;
    display: inline-flex;
    align-items: center;
    gap: 8px;
    padding: 9px 18px;
    border-radius: 50px;
    background: linear-gradient(90deg, #6c63ff 0%, #9b59f5 100%);
    color: #ffffff;
    font-family: var(--font-body);
    font-size: 13px;
    font-weight: 600;
    letter-spacing: 0.3px;
    box-shadow: 0 8px 25px rgba(108, 99, 255, 0.55), 0 0 15px rgba(155, 89, 245, 0.4);
    opacity: 0;
    scale: 0.8;
    transition: opacity 0.22s ease, scale 0.22s ease;
    will-change: transform;
}
.figma-cursor-tooltip.is-active {
    opacity: 1;
    scale: 1;
}
.tooltip-figma-icon {
    width: 13px;
    height: 13px;
    fill: currentColor;
}

@media screen and (max-width: 768px) {
    .projects-grid {
        grid-template-columns: 1fr;
    }
}
</style>