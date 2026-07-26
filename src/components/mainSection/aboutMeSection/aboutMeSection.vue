<script setup>
import { onMounted } from 'vue';

onMounted(()=> {
    const Observer = new IntersectionObserver((entries)=> {
        entries.forEach(entry => {
            if (entry.isIntersecting) {
                entry.target.classList.add('active--s');
                Observer.unobserve(entry.target);         
            }
        });
        }, {
            rootMargin: '-25% 0px -25% 0px'
    });

    let aboutItems = document.querySelector('.aboutMe--wrapper');
    if(aboutItems) Observer.observe(aboutItems);
});
</script>

<template>
    <div class="aboutMe--wrapper">
        <div class="container">
            
            <div class="metrics--wrapper">
                <div class="metric-card">
                    <div class="icon-box">
                        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="m-icon">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M12 6v6h4.5m4.5 0a9 9 0 1 1-18 0 9 9 0 0 1 18 0Z" />
                        </svg>
                    </div>
                    <div class="m-text">
                        <h3>3+</h3>
                        <p>Years experience</p>
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
                        <p>Projects Completed</p>
                    </div>
                </div>
                <div class="metric-card">
                    <div class="icon-box" style="color: #b053e0; background: rgba(176, 83, 224, 0.1);">
                        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="m-icon">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M11.42 15.17 17.25 21A2.652 2.652 0 0 0 21 17.25l-5.877-5.877M11.42 15.17l2.496-3.03c.317-.384.74-.626 1.208-.766M11.42 15.17l-4.655 5.653a2.548 2.548 0 1 1-3.586-3.586l6.837-5.63m5.108-.233c.55-.164 1.163-.188 1.743-.14a4.5 4.5 0 0 0 4.486-6.336l-3.276 3.277a3.004 3.004 0 0 1-2.25-2.25l3.276-3.276a4.5 4.5 0 0 0-6.336 4.486c.091 1.076-.071 2.264-.904 2.95l-.102.085m-1.745 1.437L5.909 7.5H4.5L2.25 3.75l1.5-1.5L7.5 4.5v1.409l4.26 4.26m-1.745 1.437 1.745-1.437m6.615 8.206L15.75 15.75M4.867 19.125h.008v.008h-.008v-.008Z" />
                        </svg>
                    </div>
                    <div class="m-text">
                        <h3>+5</h3>
                        <p>Tools Mastered</p>
                    </div>
                </div>
                <div class="metric-card">
                    <div class="icon-box" style="color: #d1416e; background: rgba(209, 65, 110, 0.1);">
                        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="m-icon">
                            <path d="M4.26 10.147a60.438 60.438 0 0 0-.491 6.347A48.62 48.62 0 0 1 12 20.904a48.62 48.62 0 0 1 8.232-4.41 60.46 60.46 0 0 0-.491-6.347m-15.482 0a50.636 50.636 0 0 0-2.658-.813A59.906 59.906 0 0 1 12 3.493a59.903 59.903 0 0 1 10.399 5.84c-.896.248-1.783.52-2.658.814m-15.482 0A50.717 50.717 0 0 1 12 13.489a50.702 50.702 0 0 1 7.74-3.342M6.75 15a.75.75 0 1 0 0-1.5.75.75 0 0 0 0 1.5Zm0 0v-3.675A55.378 55.378 0 0 1 12 8.443m-7.007 11.55A5.981 5.981 0 0 0 6.75 15.75v-1.5" stroke-linecap="round" stroke-linejoin="round"/>
                        </svg>
                    </div>
                    <div class="m-text">
                        <h3>BSc</h3>
                        <p>Computer Engineering</p>
                    </div>
                </div>
            </div>

            <div class="heading--wrapper">
                <h1 class="heading">About Me</h1>
            </div>

            <div class="aboutContent--layout">
                <div class="about-left">
                    <h2 class="hero-title">
                        <span class="hero-title-top">Designing digital products</span>
                        <span class="hero-title-main highlight-purple">that people actually love.</span>
                    </h2>
                    <p class="about-desc">I spend my days turning complex ideas into clean, eye-catching apps and websites that just make sense. My goal is simple: to design beautiful, smooth layouts that people actually enjoy using every single day, keeping everything clean and perfectly straightforward. <span class="highlight-gradient">Wanna know me Better?</span></p>
                    <a href="/resumes/ResumeEnglish.pdf" download class="cta-btn cta-btn--primary" id="about-download-cv-btn">
                        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="btn-icon">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M3 16.5v2.25A2.25 2.25 0 0 0 5.25 21h13.5A2.25 2.25 0 0 0 21 18.75V16.5M16.5 12 12 16.5m0 0L7.5 12m4.5 4.5V3" />
                        </svg>
                        <span class="btn-label">Download CV</span>
                    </a>
                </div>
                
                <div class="about-right">
                    <div class="details-grid">
                        <div class="detail-item">
                            <div class="detail-icon">
                                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6"><path stroke-linecap="round" stroke-linejoin="round" d="M6.75 3v2.25M17.25 3v2.25M3 18.75V7.5a2.25 2.25 0 0 1 2.25-2.25h13.5A2.25 2.25 0 0 1 21 7.5v11.25m-18 0A2.25 2.25 0 0 0 5.25 21h13.5A2.25 2.25 0 0 0 21 18.75m-18 0v-7.5A2.25 2.25 0 0 1 5.25 9h13.5A2.25 2.25 0 0 1 21 11.25v7.5" /></svg>
                            </div>
                            <div class="detail-text">
                                <span>Designer Since</span>
                                <strong>July 2023</strong>
                            </div>
                        </div>
                        <div class="detail-item">
                            <div class="detail-icon">
                                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6"><path stroke-linecap="round" stroke-linejoin="round" d="M15.75 6a3.75 3.75 0 1 1-7.5 0 3.75 3.75 0 0 1 7.5 0ZM4.501 20.118a7.5 7.5 0 0 1 14.998 0A17.933 17.933 0 0 1 12 21.75c-2.676 0-5.216-.584-7.499-1.632Z" /></svg>
                            </div>
                            <div class="detail-text">
                                <span>Available For</span>
                                <strong>Freelance & Full-time</strong>
                            </div>
                        </div>
                        <div class="detail-item">
                            <div class="detail-icon">
                                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6"><path stroke-linecap="round" stroke-linejoin="round" d="M15 10.5a3 3 0 1 1-6 0 3 3 0 0 1 6 0Z" /><path stroke-linecap="round" stroke-linejoin="round" d="M19.5 10.5c0 7.142-7.5 11.25-7.5 11.25S4.5 17.642 4.5 10.5a7.5 7.5 0 1 1 15 0Z" /></svg>
                            </div>
                            <div class="detail-text">
                                <span>Location</span>
                                <strong>IRAN, Sardasht</strong>
                            </div>
                        </div>
                        <div class="detail-item">
                            <div class="detail-icon">
                                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6"><path stroke-linecap="round" stroke-linejoin="round" d="M4.26 10.147a60.438 60.438 0 0 0-.491 6.347A48.62 48.62 0 0 1 12 20.904a48.62 48.62 0 0 1 8.232-4.41 60.46 60.46 0 0 0-.491-6.347m-15.482 0a50.636 50.636 0 0 0-2.658-.813A59.906 59.906 0 0 1 12 3.493a59.903 59.903 0 0 1 10.399 5.84c-.896.248-1.783.52-2.658.814m-15.482 0A50.717 50.717 0 0 1 12 13.489a50.702 50.702 0 0 1 7.74-3.342M6.75 15a.75.75 0 1 0 0-1.5.75.75 0 0 0 0 1.5Zm0 0v-3.675A55.378 55.378 0 0 1 12 8.443m-7.007 11.55A5.981 5.981 0 0 0 6.75 15.75v-1.5" /></svg>
                            </div>
                            <div class="detail-text">
                                <span>Education</span>
                                <strong>BSc Computer Engineering (GPA: 4.5)</strong>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

        </div>
    </div>
</template>

<style scoped>
/* ── Wrapper & Scroll Animations ── */
.aboutMe--wrapper {
    padding: 75px 0 60px;
}

/* Heading slides in from above */
.aboutMe--wrapper .heading--wrapper {
    opacity: 0;
    transform: translateY(-22px);
    transition: opacity 0.65s ease, transform 0.65s ease;
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
    transform: translateX(-40px);
    transition: opacity 0.75s 0.2s cubic-bezier(0.22, 1, 0.36, 1), transform 0.75s 0.2s cubic-bezier(0.22, 1, 0.36, 1);
}
.active--s .about-left {
    opacity: 1;
    transform: translateX(0);
}

/* Right card slides from right */
.about-right {
    flex: 1;
    min-width: 320px;
    opacity: 0;
    transform: translateX(40px);
    transition: opacity 0.75s 0.3s cubic-bezier(0.22, 1, 0.36, 1), transform 0.75s 0.3s cubic-bezier(0.22, 1, 0.36, 1);
}
.active--s .about-right {
    opacity: 1;
    transform: translateX(0);
}

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
    transform: translateY(20px);
    transition: opacity 0.7s 0.15s ease, transform 0.7s 0.15s ease;
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
.metric-card:last-child {
    border-right: none;
}
.metric-card:hover {
    transform: translateY(-3px);
}
.icon-box {
    background: rgba(108, 99, 255, 0.1);
    color: #6c63ff;
    padding: 12px;
    border-radius: 12px;
    display: flex;
    align-items: center;
    justify-content: center;
}
.m-icon {
    width: 28px;
    height: 28px;
}
.m-text h3 {
    font-size: 24px;
    color: #fff;
    margin: 0;
    font-weight: 700;
}
.m-text p {
    font-size: 14px;
    color: rgba(255, 255, 255, 0.6);
    margin: 0;
}

.heading--wrapper {
    text-align: center;
    margin-bottom: 50px;
}
.heading {
    display: inline-block;
    color: #fff;
    font-family: var(--font-display);
    border-bottom: 4px solid #6c63ff;
    letter-spacing: 1px;
    padding-bottom: 5px;
}

.aboutContent--layout {
    display: flex;
    flex-wrap: wrap;
    gap: 40px;
    justify-content: space-between;
    align-items: center;
}

.about-left {
    flex: 1;
    min-width: 300px;
}
.hero-title {
    display: flex;
    flex-direction: column;
    margin-bottom: 20px;
    line-height: 1.25;
    font-family: var(--font-display);
}
.hero-title-top {
    font-size: 22px;
    font-weight: 400;
    color: rgba(255, 255, 255, 0.85);
    margin-bottom: 6px;
}
.hero-title-main {
    font-size: clamp(28px, 4vw, 38px);
    font-weight: 700;
    background: linear-gradient(90deg, #6c63ff 0%, #9b59f5 100%);
    -webkit-background-clip: text;
    background-clip: text;
    color: transparent;
}
.highlight-purple {
    background: linear-gradient(90deg, #6c63ff 0%, #9b59f5 100%);
    -webkit-background-clip: text;
    background-clip: text;
    color: transparent;
}
.highlight-gradient {
    background: linear-gradient(90deg, #6c63ff 0%, #9b59f5 100%);
    -webkit-background-clip: text;
    background-clip: text;
    color: transparent;
    font-weight: 600;
}
.about-desc {
    font-size: 16px;
    color: rgba(255, 255, 255, 0.7);
    line-height: 1.7;
    margin-bottom: 34px;
}

.btn-icon {
    width: 18px;
    height: 18px;
}

.about-right {
    flex: 1;
    min-width: 320px;
    background: rgba(18, 17, 43, 0.55);
    border: 1px solid rgba(255, 255, 255, 0.08);
    border-radius: 20px;
    padding: 42px 36px;
    box-shadow: 0 16px 45px rgba(0, 0, 0, 0.45), 0 0 25px rgba(108, 99, 255, 0.12);
    backdrop-filter: blur(12px);
    display: flex;
    align-items: center;
}
.details-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 36px 32px;
    width: 100%;
}
.detail-item {
    display: flex;
    align-items: flex-start;
    gap: 14px;
}
.detail-icon {
    color: #6c63ff;
    background: rgba(108, 99, 255, 0.12);
    padding: 10px;
    border-radius: 10px;
    display: flex;
}
.detail-icon svg {
    width: 22px;
    height: 22px;
}
.detail-text {
    display: flex;
    flex-direction: column;
}
.detail-text span {
    font-size: 13px;
    color: rgba(255, 255, 255, 0.55);
    margin-bottom: 4px;
}
.detail-text strong {
    font-size: 15px;
    color: #fff;
    font-weight: 600;
}

@media screen and (max-width: 768px) {
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
    .metric-card:last-child {
        border-bottom: none;
        padding-bottom: 0;
    }
    .details-grid {
        grid-template-columns: 1fr;
    }
}
</style>