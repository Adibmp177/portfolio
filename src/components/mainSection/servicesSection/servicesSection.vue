<script setup>
import { onMounted } from 'vue';

onMounted(() => {
    const Observer = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
            if (entry.isIntersecting) {
                entry.target.classList.add('active--s');

                // Stagger skill cards — slower, more cinematic
                const cards = entry.target.querySelectorAll('.skill-card');
                cards.forEach((card, i) => {
                    setTimeout(() => card.classList.add('card--visible'), 120 + i * 180);
                });

                // Stagger tag pills after cards finish
                const pills = entry.target.querySelectorAll('.tag-pill');
                pills.forEach((pill, i) => {
                    setTimeout(() => pill.classList.add('pill--visible'), 700 + i * 60);
                });

                Observer.unobserve(entry.target);
            }
        });
    }, {
        rootMargin: '-10% 0px -10% 0px'
    });

    let skillsItems = document.querySelector('.skills--wrapper');
    if (skillsItems) Observer.observe(skillsItems);
});
</script>

<template>
    <div class="skills--wrapper">
        <div class="container">
            
            <!-- Section Heading -->
            <div class="heading--wrapper">
                <h2 class="heading">My Skills</h2>
            </div>

            <!-- Top 3 Skill Cards Grid -->
            <div class="main-skills-grid">
                
                <!-- Card 1: Figma -->
                <div class="skill-card">
                    <div class="card-top">
                        <div class="s-icon figma-icon">
                            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round">
                                <path d="M5 5.5A3.5 3.5 0 0 1 8.5 2H12v7H8.5A3.5 3.5 0 0 1 5 5.5z"/>
                                <path d="M12 2h3.5a3.5 3.5 0 1 1 0 7H12V2z"/>
                                <path d="M12 12.5a3.5 3.5 0 1 1 7 0 3.5 3.5 0 1 1-7 0z"/>
                                <path d="M5 19.5A3.5 3.5 0 0 1 8.5 16H12v3.5a3.5 3.5 0 1 1-7 0z"/>
                                <path d="M5 12.5A3.5 3.5 0 0 1 8.5 9H12v7H8.5A3.5 3.5 0 0 1 5 12.5z"/>
                            </svg>
                        </div>
                    </div>
                    
                    <div class="card-header-row">
                        <h3 class="skill-title">Figma</h3>
                        <span class="badge">Advanced</span>
                    </div>

                    <div class="progress-bar-track">
                        <div class="progress-fill" style="width: 100%;"></div>
                    </div>

                    <p class="skill-desc">My main tool, UI design, prototyping, and building design systems.</p>
                </div>

                <!-- Card 2: Photoshop -->
                <div class="skill-card">
                    <div class="card-top">
                        <div class="s-icon ps-icon">
                            <span>Ps</span>
                        </div>
                    </div>
                    
                    <div class="card-header-row">
                        <h3 class="skill-title">Photoshop</h3>
                        <span class="badge">Intermediate</span>
                    </div>

                    <div class="progress-bar-track">
                        <div class="progress-fill" style="width: 75%;"></div>
                    </div>

                    <p class="skill-desc">Photo editing and compositing for visual assets and mockups.</p>
                </div>

                <!-- Card 3: AI & Prompting -->
                <div class="skill-card">
                    <div class="card-top">
                        <div class="s-icon ai-icon">
                            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor">
                                <path stroke-linecap="round" stroke-linejoin="round" d="M9.813 15.904 9 18.75l-.813-2.846a4.5 4.5 0 0 0-3.09-3.09L2.25 12l2.846-.813a4.5 4.5 0 0 0 3.09-3.09L9 5.25l.813 2.846a4.5 4.5 0 0 0 3.09 3.09l2.846.813-2.846.813a4.5 4.5 0 0 0-3.09 3.09ZM18.259 8.715 18 9.75l-.259-1.035a3.375 3.375 0 0 0-2.455-2.456L14.25 6l1.036-.259a3.375 3.375 0 0 0 2.455-2.456L18 2.25l.259 1.035a3.375 3.375 0 0 0 2.456 2.456L21.75 6l-1.035.259a3.375 3.375 0 0 0-2.456 2.456ZM16.894 20.567 16.5 21.75l-.394-1.183a2.25 2.25 0 0 0-1.423-1.423L13.5 18.75l1.183-.394a2.25 2.25 0 0 0 1.423-1.423l.394-1.183.394 1.183a2.25 2.25 0 0 0 1.423 1.423l1.183.394-1.183.394a2.25 2.25 0 0 0-1.423 1.423Z" />
                            </svg>
                        </div>
                    </div>
                    
                    <div class="card-header-row">
                        <h3 class="skill-title">AI & Prompting</h3>
                        <span class="badge">Proficient</span>
                    </div>

                    <div class="progress-bar-track">
                        <div class="progress-fill" style="width: 85%;"></div>
                    </div>

                    <p class="skill-desc">Using AI tools to speed up research, ideation, and rapid prototyping.</p>
                    
                    <div class="sub-tags">
                        <span class="sub-tag">Claude</span>
                        <span class="sub-tag">Gemini</span>
                        <span class="sub-tag">Figma AI</span>
                        <span class="sub-tag">stitch</span>
                    </div>
                </div>

            </div>

            <!-- Additional Skills Section -->
            <div class="additional-skills-container">
                <h3 class="add-skills-main-title">Additional Skills</h3>

                <!-- Category 1: UI/UX Related -->
                <div class="skill-category">
                    <h4 class="category-title">UI/UX Related</h4>
                    <div class="tags-group">
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

                <!-- Category 2: Soft Skills -->
                <div class="skill-category">
                    <h4 class="category-title">Soft Skills</h4>
                    <div class="tags-group">
                        <span class="tag-pill">Empathy</span>
                        <span class="tag-pill">Problem Solving</span>
                        <span class="tag-pill">Time Manager</span>
                        <span class="tag-pill">Team-Work</span>
                        <span class="tag-pill">Communication</span>
                    </div>
                </div>

                <!-- Category 3: Programming -->
                <div class="skill-category">
                    <h4 class="category-title">Programming</h4>
                    <div class="tags-group">
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
/* ── Wrapper & Scroll Animations ── */
.skills--wrapper {
    padding: 70px 0;
}

/* Heading slides down when section enters */
.skills--wrapper .heading--wrapper {
    opacity: 0;
    transform: translateY(-24px);
    transition: opacity 0.8s cubic-bezier(0.22, 1, 0.36, 1), transform 0.8s cubic-bezier(0.22, 1, 0.36, 1);
}
.active--s .heading--wrapper {
    opacity: 1;
    transform: translateY(0);
}

/* ── Top 3 Cards Grid ── */
.main-skills-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(310px, 1fr));
    gap: 28px;
    margin-bottom: 65px;
}

.skill-card {
    background: rgba(18, 17, 43, 0.45);
    border: 1px solid rgba(255, 255, 255, 0.07);
    border-radius: 18px;
    padding: 28px 24px;
    display: flex;
    flex-direction: column;
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.25);
    backdrop-filter: blur(8px);
    opacity: 0;
    transform: translateY(40px);
    transition:
        opacity 0.85s cubic-bezier(0.22, 1, 0.36, 1),
        transform 0.85s cubic-bezier(0.22, 1, 0.36, 1),
        border-color 0.3s ease,
        box-shadow 0.3s ease,
        background 0.3s ease;
}
.skill-card.card--visible {
    opacity: 1;
    transform: translateY(0);
}
.skill-card.card--visible:hover {
    transform: translateY(-5px);
    border-color: rgba(108, 99, 255, 0.35);
    box-shadow: 0 16px 40px rgba(0, 0, 0, 0.4), 0 0 20px rgba(108, 99, 255, 0.12);
    background: rgba(22, 20, 52, 0.55);
}

/* Icons */
.card-top {
    margin-bottom: 18px;
}
.s-icon {
    width: 44px;
    height: 44px;
    border-radius: 12px;
    display: flex;
    align-items: center;
    justify-content: center;
    background: rgba(255, 255, 255, 0.04);
    border: 1px solid rgba(255, 255, 255, 0.08);
}
.figma-icon {
    color: #a78bfa;
    background: rgba(167, 139, 250, 0.08);
}
.figma-icon svg {
    width: 20px;
    height: 20px;
}
.ps-icon {
    color: #38bdf8;
    background: rgba(56, 189, 248, 0.08);
    font-weight: 700;
    font-size: 17px;
    font-family: var(--font-body);
}
.ai-icon {
    color: #34d399;
    background: rgba(52, 211, 153, 0.08);
}
.ai-icon svg {
    width: 22px;
    height: 22px;
}

/* Header Row: Title & Badge */
.card-header-row {
    display: flex;
    align-items: center;
    justify-content: space-between;
}
.skill-title {
    font-family: var(--font-display);
    font-size: 22px;
    font-weight: 600;
    color: #ffffff;
    margin: 0;
}
.badge {
    font-size: 12px;
    font-weight: 400;
    color: rgba(255, 255, 255, 0.6);
    background: rgba(255, 255, 255, 0.03);
    border: 1px solid rgba(255, 255, 255, 0.12);
    border-radius: 50px;
    padding: 3px 12px;
}

/* Progress Bar Track & Fill */
.progress-bar-track {
    width: 100%;
    height: 3px;
    background: rgba(255, 255, 255, 0.08);
    border-radius: 2px;
    margin: 16px 0 18px 0;
    position: relative;
    overflow: hidden;
}
.progress-fill {
    height: 100%;
    background: linear-gradient(90deg, #6c63ff 0%, #9b59f5 100%);
    border-radius: 2px;
    transition: width 1s ease-in-out;
}

/* Description */
.skill-desc {
    font-size: 14px;
    color: rgba(255, 255, 255, 0.65);
    line-height: 1.6;
    margin: 0;
}

/* Sub-tags in Card 3 */
.sub-tags {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
    margin-top: 18px;
}
.sub-tag {
    font-size: 12px;
    color: rgba(255, 255, 255, 0.75);
    background: rgba(255, 255, 255, 0.04);
    border: 1px solid rgba(255, 255, 255, 0.08);
    border-radius: 50px;
    padding: 3px 12px;
}

/* ── Additional Skills Section ── */
.additional-skills-container {
    text-align: center;
    margin-top: 50px;
}
.add-skills-main-title {
    font-family: var(--font-display);
    font-size: 24px;
    font-weight: 600;
    color: #ffffff;
    margin-bottom: 35px;
}

.skill-category {
    margin-bottom: 32px;
}
.category-title {
    font-size: 16px;
    font-weight: 500;
    color: #7c6cf5;
    margin-bottom: 16px;
}

.tags-group {
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    justify-content: center;
    gap: 12px;
    max-width: 900px;
    margin: 0 auto;
}

.tag-pill {
    font-size: 14px;
    color: rgba(255, 255, 255, 0.85);
    background: rgba(255, 255, 255, 0.03);
    border: 1px solid rgba(255, 255, 255, 0.09);
    border-radius: 50px;
    padding: 8px 22px;
    cursor: default;
    user-select: none;
    opacity: 0;
    transform: scale(0.88) translateY(12px);
    transition:
        opacity 0.55s cubic-bezier(0.22, 1, 0.36, 1),
        transform 0.55s cubic-bezier(0.34, 1.56, 0.64, 1),
        border-color 0.25s ease,
        background 0.25s ease,
        color 0.25s ease,
        box-shadow 0.25s ease;
}
.tag-pill.pill--visible {
    opacity: 1;
    transform: scale(1) translateY(0);
}
.tag-pill.pill--visible:hover {
    transform: scale(1) translateY(-3px);
    border-color: rgba(108, 99, 255, 0.55);
    background: rgba(108, 99, 255, 0.14);
    color: #ffffff;
    box-shadow: 0 6px 18px rgba(108, 99, 255, 0.2);
}

/* Responsive */
@media screen and (max-width: 768px) {
    .main-skills-grid {
        grid-template-columns: 1fr;
    }
    .tags-group {
        gap: 8px;
    }
    .tag-pill {
        font-size: 13px;
        padding: 6px 16px;
    }
}
</style>