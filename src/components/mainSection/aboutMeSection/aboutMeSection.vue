<script setup>
import { onMounted } from 'vue';

onMounted(()=> {
    const Observer = new IntersectionObserver((entries)=> {
        entries.forEach(entry => {
            if (entry.isIntersecting) {
                entry.target.classList.add('active--s');

                // Stagger philosophy cards
                const cards = entry.target.querySelectorAll('.philosophy-card');
                cards.forEach((card, i) => {
                    setTimeout(() => card.classList.add('card--in'), 400 + i * 150);
                });

                Observer.unobserve(entry.target);
            }
        });
        }, {
            rootMargin: '-10% 0px -10% 0px'
    });

    let aboutItems = document.querySelector('.aboutMe--wrapper');
    if(aboutItems) Observer.observe(aboutItems);
});
</script>

<template>
    <div class="aboutMe--wrapper">
        <div class="container">
            
            <!-- Metrics Bar -->
            <div class="metrics--wrapper">
                <div class="metric-card">
                    <div class="icon-box">
                        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="m-icon">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M12 6v6h4.5m4.5 0a9 9 0 1 1-18 0 9 9 0 0 1 18 0Z" />
                        </svg>
                    </div>
                    <div class="m-text">
                        <h3>3+</h3>
                        <p>Years Experience</p>
                    </div>
                </div>
                <div class="metric-card">
                    <div class="icon-box" style="color: #c94b96; background: rgba(201, 75, 150, 0.1);">
                        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="m-icon">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M6 6.878V6a2.25 2.25 0 0 1 2.25-2.25h7.5A2.25 2.25 0 0 1 18 6v.878m-12 0c.235-.083.487-.128.75-.128h10.5c.263 0 .515.045.75.128m-12 0A2.25 2.25 0 0 0 4.5 9v.878m13.5-3A2.25 2.25 0 0 1 19.5 9v.878m0 0a2.246 2.246 0 0 0-.75-.128H5.25c-.263 0-.515.045-.75.128m15 0A2.25 2.25 0 0 1 21 12v6a2.25 2.25 0 0 1-2.25 2.25H5.25A2.25 2.25 0 0 1 3 18v-6c0-.98.626-1.813 1.5-2.122" />
                        </svg>
                    </div>
                    <div class="m-text">
                        <h3>12+</h3>
                        <p>Projects Shipped</p>
                    </div>
                </div>
                <div class="metric-card">
                    <div class="icon-box" style="color: #34d399; background: rgba(52, 211, 153, 0.1);">
                        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="m-icon">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M15.75 6a3.75 3.75 0 1 1-7.5 0 3.75 3.75 0 0 1 7.5 0ZM4.501 20.118a7.5 7.5 0 0 1 14.998 0A17.933 17.933 0 0 1 12 21.75c-2.676 0-5.216-.584-7.499-1.632Z" />
                        </svg>
                    </div>
                    <div class="m-text">
                        <h3>100%</h3>
                        <p>User-Centered</p>
                    </div>
                </div>
                <div class="metric-card">
                    <div class="icon-box" style="color: #f59e0b; background: rgba(245, 158, 11, 0.1);">
                        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="m-icon">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M4.26 10.147a60.438 60.438 0 0 0-.491 6.347A48.62 48.62 0 0 1 12 20.904a48.62 48.62 0 0 1 8.232-4.41 60.46 60.46 0 0 0-.491-6.347m-15.482 0a50.636 50.636 0 0 0-2.658-.813A59.906 59.906 0 0 1 12 3.493a59.903 59.903 0 0 1 10.399 5.84c-.896.248-1.783.52-2.658.814m-15.482 0A50.717 50.717 0 0 1 12 13.489a50.702 50.702 0 0 1 7.74-3.342M6.75 15a.75.75 0 1 0 0-1.5.75.75 0 0 0 0 1.5Zm0 0v-3.675A55.378 55.378 0 0 1 12 8.443m-7.007 11.55A5.981 5.981 0 0 0 6.75 15.75v-1.5" />
                        </svg>
                    </div>
                    <div class="m-text">
                        <h3>BSc</h3>
                        <p>Computer Engineering</p>
                    </div>
                </div>
            </div>

            <!-- Section Heading -->
            <div class="heading--wrapper">
                <h1 class="heading">About Me</h1>
            </div>

            <!-- Main Content Layout -->
            <div class="aboutContent--layout">

                <!-- Left: Avatar + Story -->
                <div class="about-left">

                    <!-- Avatar Card -->
                    <div class="avatar-card">
                        <div class="avatar-ring">
                            <img
                                src="/images/profile.webp"
                                alt="Adib Mohammad Pouri"
                                class="avatar-photo"
                                onerror="this.style.display='none'; this.nextElementSibling.style.display='flex';"
                            />
                            <div class="avatar-initials" style="display:none">AM</div>
                        </div>
                        <div class="avatar-info">
                            <p class="avatar-name">Adib Mohammad Pouri</p>
                            <p class="avatar-role">UI/UX Designer</p>
                            <span class="available-badge">
                                <span class="badge-dot"></span>
                                Available for work
                            </span>
                        </div>
                    </div>

                    <!-- Personal Story -->
                    <div class="story-block">
                        <h2 class="story-title">
                            <span class="story-top">I don't just design screens,</span>
                            <span class="story-gradient">I shape how people feel.</span>
                        </h2>
                        <p class="story-p">
                            Born curious, raised on code, and obsessed with the space where logic meets beauty. I got into design because I kept asking <em>"why is this so frustrating to use?"</em>, and realized I wanted to be the one who fixes that.
                        </p>
                        <p class="story-p">
                            Every project starts with one question: <strong>what does the user actually need?</strong> Not what the brief says, not what looks impressive in a mockup, but what genuinely makes their life easier. That obsession drives every decision I make.
                        </p>

                        <div class="cta-row">
                            <a href="/resumes/ResumeEnglish.pdf" download class="cta-btn cta-btn--primary" id="about-download-cv-btn">
                                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="btn-icon">
                                    <path stroke-linecap="round" stroke-linejoin="round" d="M3 16.5v2.25A2.25 2.25 0 0 0 5.25 21h13.5A2.25 2.25 0 0 0 21 18.75V16.5M16.5 12 12 16.5m0 0L7.5 12m4.5 4.5V3" />
                                </svg>
                                <span class="btn-label">Download CV</span>
                            </a>
                            <a href="#contact" class="cta-btn cta-btn--outline" id="about-contact-btn">
                                <span class="btn-label">Let's Talk</span>
                            </a>
                        </div>
                    </div>
                </div>

                <!-- Right: Details + Philosophy -->
                <div class="about-right">

                    <!-- Quick Facts -->
                    <div class="facts-card">
                        <p class="facts-title">Quick Facts</p>
                        <div class="details-grid">
                            <div class="detail-item">
                                <div class="detail-icon">
                                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" d="M6.75 3v2.25M17.25 3v2.25M3 18.75V7.5a2.25 2.25 0 0 1 2.25-2.25h13.5A2.25 2.25 0 0 1 21 7.5v11.25m-18 0A2.25 2.25 0 0 0 5.25 21h13.5A2.25 2.25 0 0 0 21 18.75m-18 0v-7.5A2.25 2.25 0 0 1 5.25 9h13.5A2.25 2.25 0 0 1 21 11.25v7.5" /></svg>
                                </div>
                                <div class="detail-text">
                                    <span>Designer Since</span>
                                    <strong>July 2023</strong>
                                </div>
                            </div>
                            <div class="detail-item">
                                <div class="detail-icon">
                                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" d="M15.75 6a3.75 3.75 0 1 1-7.5 0 3.75 3.75 0 0 1 7.5 0ZM4.501 20.118a7.5 7.5 0 0 1 14.998 0A17.933 17.933 0 0 1 12 21.75c-2.676 0-5.216-.584-7.499-1.632Z" /></svg>
                                </div>
                                <div class="detail-text">
                                    <span>Available For</span>
                                    <strong>Freelance &amp; Full-time</strong>
                                </div>
                            </div>
                            <div class="detail-item">
                                <div class="detail-icon">
                                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" d="M15 10.5a3 3 0 1 1-6 0 3 3 0 0 1 6 0Z" /><path stroke-linecap="round" stroke-linejoin="round" d="M19.5 10.5c0 7.142-7.5 11.25-7.5 11.25S4.5 17.642 4.5 10.5a7.5 7.5 0 1 1 15 0Z" /></svg>
                                </div>
                                <div class="detail-text">
                                    <span>Location</span>
                                    <strong>IRAN, Sardasht</strong>
                                </div>
                            </div>
                            <div class="detail-item">
                                <div class="detail-icon">
                                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" d="M4.26 10.147a60.438 60.438 0 0 0-.491 6.347A48.62 48.62 0 0 1 12 20.904a48.62 48.62 0 0 1 8.232-4.41 60.46 60.46 0 0 0-.491-6.347m-15.482 0a50.636 50.636 0 0 0-2.658-.813A59.906 59.906 0 0 1 12 3.493a59.903 59.903 0 0 1 10.399 5.84c-.896.248-1.783.52-2.658.814m-15.482 0A50.717 50.717 0 0 1 12 13.489a50.702 50.702 0 0 1 7.74-3.342M6.75 15a.75.75 0 1 0 0-1.5.75.75 0 0 0 0 1.5Zm0 0v-3.675A55.378 55.378 0 0 1 12 8.443m-7.007 11.55A5.981 5.981 0 0 0 6.75 15.75v-1.5" /></svg>
                                </div>
                                <div class="detail-text">
                                    <span>Education</span>
                                    <strong>BSc Computer Eng. (GPA 4.5)</strong>
                                </div>
                            </div>
                        </div>
                    </div>

                    <!-- Design Philosophy Cards -->
                    <div class="philosophy-section">
                        <p class="philosophy-label">My Design Beliefs</p>
                        <div class="philosophy-grid">
                            <div class="philosophy-card">
                                <span class="ph-icon">&#10022;</span>
                                <p><strong>Clarity over cleverness.</strong> If a user has to think, I've already failed.</p>
                            </div>
                            <div class="philosophy-card">
                                <span class="ph-icon">&#10022;</span>
                                <p><strong>Details are the design.</strong> What looks simple usually took the most time.</p>
                            </div>
                            <div class="philosophy-card">
                                <span class="ph-icon">&#10022;</span>
                                <p><strong>Empathy first, aesthetics second.</strong> Beautiful but unusable is just art.</p>
                            </div>
                        </div>
                    </div>

                </div>
            </div>

        </div>
    </div>
</template>

<style scoped>
/* â”€â”€ Wrapper & Scroll Animations â”€â”€ */
.aboutMe--wrapper {
    position: relative;
    padding: 90px 0 95px;
}

/* Glowing purple divider line at the exact boundary between Hero and About Me */
.aboutMe--wrapper::before {
    content: '';
    display: block;
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 1px;
    background: linear-gradient(90deg, transparent 0%, rgba(108, 99, 255, 0.55) 30%, rgba(155, 89, 245, 0.55) 50%, rgba(108, 99, 255, 0.55) 70%, transparent 100%);
    box-shadow: 0 0 14px rgba(108, 99, 255, 0.5);
}

/* Heading slides in from above */
.aboutMe--wrapper .heading--wrapper {
    opacity: 0;
    transform: translateY(-24px);
    transition: opacity 0.8s cubic-bezier(0.22, 1, 0.36, 1), transform 0.8s cubic-bezier(0.22, 1, 0.36, 1);
}
.active--s .heading--wrapper {
    opacity: 1;
    transform: translateY(0);
}

/* Left column slides from left */
.about-left {
    flex: 1;
    min-width: 300px;
    opacity: 0;
    transform: translateX(-50px);
    transition: opacity 0.9s 0.15s cubic-bezier(0.22, 1, 0.36, 1), transform 0.9s 0.15s cubic-bezier(0.22, 1, 0.36, 1);
}
.active--s .about-left {
    opacity: 1;
    transform: translateX(0);
}

/* Right card slides from right */
.about-right {
    flex: 1.05;
    min-width: 320px;
    opacity: 0;
    transform: translateX(50px);
    transition: opacity 0.9s 0.3s cubic-bezier(0.22, 1, 0.36, 1), transform 0.9s 0.3s cubic-bezier(0.22, 1, 0.36, 1);
}
.active--s .about-right {
    opacity: 1;
    transform: translateX(0);
}

/* â”€â”€ Metrics Bar â”€â”€ */
.metrics--wrapper {
    display: flex;
    align-items: center;
    justify-content: space-between;
    background: rgba(18, 17, 43, 0.6);
    border: 1px solid rgba(255, 255, 255, 0.08);
    border-radius: 22px;
    padding: 26px 36px;
    margin-bottom: 85px;
    box-shadow: 0 16px 45px rgba(0, 0, 0, 0.45), 0 0 35px rgba(108, 99, 255, 0.15);
    backdrop-filter: blur(14px);
    width: 100%;
    opacity: 0;
    transform: translateY(28px);
    transition: opacity 0.85s cubic-bezier(0.22, 1, 0.36, 1), transform 0.85s cubic-bezier(0.22, 1, 0.36, 1);
}
.active--s .metrics--wrapper {
    opacity: 1;
    transform: translateY(0);
}
.metric-card {
    display: flex;
    align-items: center;
    gap: 16px;
    flex: 1;
    justify-content: center;
    padding: 0 15px;
    border-right: 1px solid rgba(255, 255, 255, 0.08);
    transition: transform 0.3s ease;
}
.metric-card:last-child { border-right: none; }
.metric-card:hover { transform: translateY(-3px); }
.icon-box {
    background: rgba(108, 99, 255, 0.1);
    color: #6c63ff;
    padding: 12px;
    border-radius: 12px;
    display: flex;
    align-items: center;
    justify-content: center;
}
.m-icon { width: 28px; height: 28px; }
.m-text h3 { font-size: 24px; color: #fff; margin: 0; font-weight: 700; }
.m-text p  { font-size: 14px; color: rgba(255,255,255,0.6); margin: 0; }

/* â”€â”€ Heading â”€â”€ */
.heading--wrapper { text-align: center; margin-bottom: 55px; }
.heading {
    display: inline-block;
    color: #fff;
    font-family: var(--font-display);
    border-bottom: 4px solid #6c63ff;
    letter-spacing: 1px;
    padding-bottom: 5px;
}

/* â”€â”€ Main Layout â”€â”€ */
.aboutContent--layout {
    display: flex;
    flex-wrap: wrap;
    gap: 44px;
    justify-content: space-between;
    align-items: flex-start;
}

/* â”€â”€ LEFT SIDE â”€â”€ */

.avatar-card {
    display: flex;
    align-items: center;
    gap: 18px;
    background: rgba(18, 17, 43, 0.5);
    border: 1px solid rgba(255, 255, 255, 0.08);
    border-radius: 18px;
    padding: 20px 24px;
    margin-bottom: 30px;
    backdrop-filter: blur(10px);
    box-shadow: 0 8px 30px rgba(0,0,0,0.3), 0 0 15px rgba(108, 99, 255, 0.08);
}
.avatar-ring {
    width: 62px;
    height: 62px;
    border-radius: 50%;
    background: linear-gradient(135deg, #6c63ff 0%, #9b59f5 100%);
    display: flex;
    align-items: center;
    justify-content: center;
    box-shadow: 0 0 0 3px rgba(108, 99, 255, 0.25), 0 0 20px rgba(108, 99, 255, 0.4);
    flex-shrink: 0;
}
.avatar-initials {
    font-family: var(--font-display);
    font-size: 20px;
    font-weight: 700;
    color: #fff;
    letter-spacing: 1px;
}
.avatar-photo {
    width: 100%;
    height: 100%;
    object-fit: cover;
    border-radius: 50%;
    display: block;
}
.avatar-info { display: flex; flex-direction: column; gap: 3px; }
.avatar-name { font-size: 16px; font-weight: 600; color: #fff; margin: 0; }
.avatar-role { font-size: 13px; color: rgba(255,255,255,0.5); margin: 0; }
.available-badge {
    display: inline-flex;
    align-items: center;
    gap: 6px;
    margin-top: 5px;
    font-size: 11.5px;
    color: #34d399;
    background: rgba(52, 211, 153, 0.1);
    border: 1px solid rgba(52, 211, 153, 0.3);
    border-radius: 50px;
    padding: 3px 10px;
    width: fit-content;
}
.badge-dot {
    width: 6px;
    height: 6px;
    border-radius: 50%;
    background: #34d399;
    box-shadow: 0 0 6px rgba(52, 211, 153, 0.8);
    animation: pulse-dot 2s ease-in-out infinite;
}
@keyframes pulse-dot {
    0%, 100% { box-shadow: 0 0 6px rgba(52, 211, 153, 0.8); }
    50%       { box-shadow: 0 0 14px rgba(52, 211, 153, 1), 0 0 22px rgba(52, 211, 153, 0.4); }
}

.story-title {
    display: flex;
    flex-direction: column;
    font-family: var(--font-display);
    line-height: 1.22;
    margin-bottom: 22px;
}
.story-top {
    font-size: 20px;
    font-weight: 400;
    color: rgba(255,255,255,0.8);
    margin-bottom: 4px;
}
.story-gradient {
    font-size: clamp(26px, 3.5vw, 36px);
    font-weight: 700;
    background: linear-gradient(90deg, #6c63ff 0%, #9b59f5 100%);
    -webkit-background-clip: text;
    background-clip: text;
    color: transparent;
}
.story-p {
    font-size: 15px;
    color: rgba(255,255,255,0.68);
    line-height: 1.8;
    margin-bottom: 16px;
}
.story-p em     { color: rgba(255,255,255,0.92); font-style: italic; }
.story-p strong { color: #fff; font-weight: 600; }

.cta-row {
    display: flex;
    align-items: center;
    gap: 14px;
    margin-top: 30px;
    flex-wrap: wrap;
}
.btn-icon { width: 18px; height: 18px; }

/* â”€â”€ RIGHT SIDE â”€â”€ */

.facts-card {
    background: rgba(18, 17, 43, 0.55);
    border: 1px solid rgba(255, 255, 255, 0.08);
    border-radius: 20px;
    padding: 30px 26px;
    box-shadow: 0 16px 45px rgba(0, 0, 0, 0.45), 0 0 25px rgba(108, 99, 255, 0.1);
    backdrop-filter: blur(12px);
    margin-bottom: 22px;
}
.facts-title {
    font-size: 11px;
    font-weight: 600;
    color: rgba(255,255,255,0.4);
    text-transform: uppercase;
    letter-spacing: 1px;
    margin-bottom: 22px;
}
.details-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 26px 22px;
    width: 100%;
}
.detail-item { display: flex; align-items: flex-start; gap: 12px; }
.detail-icon {
    color: #6c63ff;
    background: rgba(108, 99, 255, 0.12);
    padding: 9px;
    border-radius: 10px;
    display: flex;
    flex-shrink: 0;
}
.detail-icon svg { width: 20px; height: 20px; }
.detail-text { display: flex; flex-direction: column; }
.detail-text span { font-size: 12px; color: rgba(255,255,255,0.5); margin-bottom: 3px; }
.detail-text strong { font-size: 14px; color: #fff; font-weight: 600; }

.philosophy-section {
    margin-top: 32px;
}
.philosophy-label {
    font-size: 11px;
    font-weight: 600;
    color: rgba(255,255,255,0.4);
    text-transform: uppercase;
    letter-spacing: 1px;
    margin-bottom: 14px;
}
.philosophy-grid { display: flex; flex-direction: column; gap: 10px; }
.philosophy-card {
    display: flex;
    align-items: flex-start;
    gap: 14px;
    background: rgba(108, 99, 255, 0.05);
    border: 1px solid rgba(108, 99, 255, 0.13);
    border-radius: 14px;
    padding: 15px 16px;
    opacity: 0;
    transform: translateX(22px);
    transition:
        opacity 0.6s cubic-bezier(0.22, 1, 0.36, 1),
        transform 0.6s cubic-bezier(0.22, 1, 0.36, 1),
        background 0.25s ease,
        border-color 0.25s ease;
}
.philosophy-card.card--in { opacity: 1; transform: translateX(0); }
.philosophy-card:hover {
    background: rgba(108, 99, 255, 0.1);
    border-color: rgba(108, 99, 255, 0.28);
}
.ph-icon { font-size: 20px; color: #9b59f5; flex-shrink: 0; margin-top: 1px; line-height: 1; }
.philosophy-card p { font-size: 13.5px; color: rgba(255,255,255,0.68); line-height: 1.6; margin: 0; }
.philosophy-card p strong { color: #fff; }

/* ── Responsive ── */
@media screen and (max-width: 768px) {
    .about-left {
        padding: 0 8px;
    }
    .metrics--wrapper {
        flex-direction: column;
        gap: 20px;
        padding: 24px 20px;
    }
    .metric-card {
        border-right: none;
        border-bottom: 1px solid rgba(255, 255, 255, 0.08);
        padding-bottom: 16px;
        width: 100%;
        justify-content: flex-start;
    }
    .metric-card:last-child { border-bottom: none; padding-bottom: 0; }
    .details-grid { grid-template-columns: 1fr; }
}

@media screen and (max-width: 480px) {
    .cta-row { flex-direction: column; width: 100%; }
    .cta-row .cta-btn { width: 100%; justify-content: center; }
    .avatar-card { flex-direction: column; text-align: center; }
    .avatar-info { align-items: center; }
}
</style>