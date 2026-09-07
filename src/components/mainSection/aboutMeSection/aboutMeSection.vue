<script setup>
import { onMounted, ref, onUnmounted } from 'vue';

// ── Metric Count-Up Animation ─────────────────────────────
const expCount = ref(0);
const projectsCount = ref(0);
const satisfactionCount = ref(0);
let animFrame = null;

function animateMetrics() {
  const duration = 1600;
  const start = performance.now();
  const targets = { exp: 3, projects: 12, satisfaction: 100 };

  function tick(now) {
    const elapsed = now - start;
    const progress = Math.min(elapsed / duration, 1);
    const ease = 1 - Math.pow(1 - progress, 3); // ease-out cubic

    expCount.value = Math.round(targets.exp * ease);
    projectsCount.value = Math.round(targets.projects * ease);
    satisfactionCount.value = Math.round(targets.satisfaction * ease);

    if (progress < 1) {
      animFrame = requestAnimationFrame(tick);
    }
  }
  animFrame = requestAnimationFrame(tick);
}

// ── Interactive Principle Selection ───────────────────────
const activePrinciple = ref(0);
const principles = [
  {
    number: "01",
    title: "Clarity Over Cleverness",
    tagline: "Frictionless intuition is true sophistication.",
    desc: "If a user has to pause and think, design has already introduced unnecessary cognitive load. Simplicity isn't the absence of clutter—it's the presence of clarity.",
    impact: "Zero onboarding friction & immediate task completion.",
    icon: "✦",
    color: "#6c63ff",
    colorRgb: "108, 99, 255"
  },
  {
    number: "02",
    title: "Systems Before Pixels",
    tagline: "Scalable tokens & modular architecture.",
    desc: "Every great product scales on unified rules. Building robust design systems with reusable components bridges the gap between design vision and engineered reality.",
    impact: "3x faster team velocity & bulletproof consistency.",
    icon: "⚡",
    color: "#9b59f5",
    colorRgb: "155, 89, 245"
  },
  {
    number: "03",
    title: "Empathy Before Aesthetics",
    tagline: "Solving real user problems with purpose.",
    desc: "A gorgeous interface that fails user goals is just decoration. Purposeful UX starts with deep listening, rigorous research, and relentless validation.",
    impact: "Measurable engagement growth & high retention.",
    icon: "♥",
    color: "#10b981",
    colorRgb: "16, 185, 129"
  }
];

onMounted(() => {
  const Observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.classList.add('active--s');
        setTimeout(animateMetrics, 300);
        Observer.unobserve(entry.target);
      }
    });
  }, {
    rootMargin: '-10% 0px -10% 0px'
  });

  const aboutItems = document.querySelector('.aboutMe--wrapper');
  if (aboutItems) Observer.observe(aboutItems);
});

onUnmounted(() => {
  if (animFrame) cancelAnimationFrame(animFrame);
});
</script>

<template>
  <div class="aboutMe--wrapper">
    <!-- Ambient Lighting Glow Orbs -->
    <div class="about-glow-orb about-glow-1"></div>
    <div class="about-glow-orb about-glow-2"></div>

    <div class="container">
      
      <!-- ═══════════════════════════════════════════════════
           1. ANIMATED LIVE METRICS DASHBOARD
      ═══════════════════════════════════════════════════ -->
      <div class="metrics--wrapper">
        <div class="metric-card metric-card--indigo">
          <div class="icon-box">
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.8" stroke="currentColor" class="m-icon">
              <path stroke-linecap="round" stroke-linejoin="round" d="M12 6v6h4.5m4.5 0a9 9 0 1 1-18 0 9 9 0 0 1 18 0Z" />
            </svg>
          </div>
          <div class="m-text">
            <h3>{{ expCount }}+</h3>
            <p>Years Experience</p>
          </div>
        </div>

        <div class="metric-card metric-card--pink">
          <div class="icon-box">
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.8" stroke="currentColor" class="m-icon">
              <path stroke-linecap="round" stroke-linejoin="round" d="M6 6.878V6a2.25 2.25 0 0 1 2.25-2.25h7.5A2.25 2.25 0 0 1 18 6v.878m-12 0c.235-.083.487-.128.75-.128h10.5c.263 0 .515.045.75.128m-12 0A2.25 2.25 0 0 0 4.5 9v.878m13.5-3A2.25 2.25 0 0 1 19.5 9v.878m0 0a2.246 2.246 0 0 0-.75-.128H5.25c-.263 0-.515.045-.75.128m15 0A2.25 2.25 0 0 1 21 12v6a2.25 2.25 0 0 1-2.25 2.25H5.25A2.25 2.25 0 0 1 3 18v-6c0-.98.626-1.813 1.5-2.122" />
            </svg>
          </div>
          <div class="m-text">
            <h3>{{ projectsCount }}+</h3>
            <p>Projects Shipped</p>
          </div>
          <span class="card-glow-reflection"></span>
        </div>

        <div class="metric-card metric-card--emerald">
          <div class="icon-box">
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.8" stroke="currentColor" class="m-icon">
              <path stroke-linecap="round" stroke-linejoin="round" d="M15.75 6a3.75 3.75 0 1 1-7.5 0 3.75 3.75 0 0 1 7.5 0ZM4.501 20.118a7.5 7.5 0 0 1 14.998 0A17.933 17.933 0 0 1 12 21.75c-2.676 0-5.216-.584-7.499-1.632Z" />
            </svg>
          </div>
          <div class="m-text">
            <h3>{{ satisfactionCount }}%</h3>
            <p>User-Centered</p>
          </div>
          <span class="card-glow-reflection"></span>
        </div>

        <div class="metric-card metric-card--amber">
          <div class="icon-box">
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.8" stroke="currentColor" class="m-icon">
              <path stroke-linecap="round" stroke-linejoin="round" d="M4.26 10.147a60.438 60.438 0 0 0-.491 6.347A48.62 48.62 0 0 1 12 20.904a48.62 48.62 0 0 1 8.232-4.41 60.46 60.46 0 0 0-.491-6.347m-15.482 0a50.636 50.636 0 0 0-2.658-.813A59.906 59.906 0 0 1 12 3.493a59.903 59.903 0 0 1 10.399 5.84c-.896.248-1.783.52-2.658.814m-15.482 0A50.717 50.717 0 0 1 12 13.489a50.702 50.702 0 0 1 7.74-3.342M6.75 15a.75.75 0 1 0 0-1.5.75.75 0 0 0 0 1.5Zm0 0v-3.675A55.378 55.378 0 0 1 12 8.443m-7.007 11.55A5.981 5.981 0 0 0 6.75 15.75v-1.5" />
            </svg>
          </div>
          <div class="m-text">
            <h3>BSc</h3>
            <p>Computer Engineering</p>
          </div>
          <span class="card-glow-reflection"></span>
        </div>
      </div>

      <!-- Section Heading -->
      <div class="heading--wrapper">
        <h2 class="heading">About Me</h2>
      </div>

      <!-- ═══════════════════════════════════════════════════
           2. MAIN CONTENT BENTO GRID
      ═══════════════════════════════════════════════════ -->
      <div class="aboutContent--layout">

        <!-- ─── LEFT COLUMN: Profile Hub & Narrative ─── -->
        <div class="about-left">

          <!-- Enhanced Glassmorphic Profile Card -->
          <div class="avatar-card-modern">
            <div class="avatar-ring-box">
              <div class="avatar-ring-glow"></div>
              <img
                src="/images/profile.webp"
                alt="Adib Mohammadpouri"
                class="avatar-photo"
                onerror="this.style.display='none'; this.nextElementSibling.style.display='flex';"
              />
              <div class="avatar-initials" style="display:none">AM</div>
            </div>

            <div class="avatar-info-modern">
              <div class="avatar-header-row">
                <h3 class="avatar-name">Adib Mohammadpouri</h3>
                <span class="live-status-pill">
                  <span class="pulse-beacon"></span>
                  Available for work
                </span>
              </div>
              <p class="avatar-title-tag">UI/UX Designer</p>
              <div class="avatar-badges-row">
                <span class="badge-mini">📍 Sardasht, Iran</span>
                <span class="badge-mini">🌐 Remote Worldwide</span>
                <span class="badge-mini">⚡ UTC+3:30</span>
              </div>
            </div>
          </div>

          <!-- Deep Narrative Story Block -->
          <div class="story-block-modern">
            <h3 class="story-title-modern">
              <span class="story-sub">Where Engineering Rigor Meets</span>
              <span class="story-highlight">Intuitive Digital Artistry.</span>
            </h3>
            
            <p class="story-text">
              Born curious and trained in <strong>Computer Engineering</strong>, I navigate the intersection where technical logic transforms into delightful user experiences. I got into design because I constantly asked <em>"why is this so frustrating to use?"</em>, and decided to build the solution.
            </p>
            <p class="story-text">
              Every interface I craft is grounded in one fundamental rule: <strong>what does the human on the other side actually need?</strong> Not just what looks striking in a static frame, but what delivers clarity, speed, and real emotional satisfaction at scale.
            </p>

            <!-- CTA Actions -->
            <div class="cta-row-modern">
              <a href="/resumes/ResumeEnglish.pdf" download class="cta-btn cta-btn--primary" id="about-download-cv-btn">
                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor" class="btn-icon">
                  <path stroke-linecap="round" stroke-linejoin="round" d="M3 16.5v2.25A2.25 2.25 0 0 0 5.25 21h13.5A2.25 2.25 0 0 0 21 18.75V16.5M16.5 12 12 16.5m0 0L7.5 12m4.5 4.5V3" />
                </svg>
                <span class="btn-label">Download Full CV</span>
              </a>
              <a href="#contact" class="cta-btn cta-btn--outline" id="about-contact-btn">
                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor" class="btn-icon">
                  <path stroke-linecap="round" stroke-linejoin="round" d="M8.625 12a.375.375 0 1 1-.75 0 .375.375 0 0 1 .75 0Zm0 0H8.25m4.125 0a.375.375 0 1 1-.75 0 .375.375 0 0 1 .75 0Zm0 0H12m4.125 0a.375.375 0 1 1-.75 0 .375.375 0 0 1 .75 0Zm0 0h-.375M21 12c0 4.556-4.03 8.25-9 8.25a9.764 9.764 0 0 1-2.555-.337A5.972 5.972 0 0 1 5.41 20.97a.75.75 0 0 1-.75-.75 4.49 4.49 0 0 1 1.09-2.888A7.838 7.838 0 0 1 3 12c0-4.556 4.03-8.25 9-8.25s9 3.694 9 8.25Z" />
                </svg>
                <span class="btn-label">Let's Connect</span>
              </a>
            </div>
          </div>
        </div>

        <!-- ─── RIGHT COLUMN: Interactive Bento Highlights ─── -->
        <div class="about-right">

          <!-- Bento Card 1: Quick Facts Matrix -->
          <div class="bento-facts-card">
            <div class="bento-header">
              <span class="bento-tag">Credentials & Details</span>
              <span class="bento-dot-indicator"></span>
            </div>
            
            <div class="facts-grid-modern">
              <div class="fact-tile">
                <div class="fact-icon-box">
                  <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.8" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M6.75 3v2.25M17.25 3v2.25M3 18.75V7.5a2.25 2.25 0 0 1 2.25-2.25h13.5A2.25 2.25 0 0 1 21 7.5v11.25m-18 0A2.25 2.25 0 0 0 5.25 21h13.5A2.25 2.25 0 0 0 21 18.75m-18 0v-7.5A2.25 2.25 0 0 1 5.25 9h13.5A2.25 2.25 0 0 1 21 11.25v7.5" />
                  </svg>
                </div>
                <div class="fact-meta">
                  <span class="fact-lbl">Experience Start</span>
                  <strong class="fact-val">July 2023</strong>
                </div>
              </div>

              <div class="fact-tile">
                <div class="fact-icon-box">
                  <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.8" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M20.25 14.15v4.25c0 1.094-.787 2.036-1.872 2.18-2.087.277-4.216.42-6.378.42s-4.291-.143-6.378-.42c-1.085-.144-1.872-1.086-1.872-2.18v-4.25m16.5 0a2.18 2.18 0 0 0 .75-1.661V8.706c0-1.081-.768-2.015-1.837-2.175a48.114 48.114 0 0 0-3.413-.387m4.5 8.006c-.194.165-.42.295-.673.38A23.978 23.978 0 0 1 12 15.75c-2.648 0-5.195-.429-7.577-1.22a2.016 2.016 0 0 1-.673-.38m0 0A2.18 2.18 0 0 1 3 12.489V8.706c0-1.081.768-2.015 1.837-2.175a48.111 48.111 0 0 1 3.413-.387m7.5 0V5.25A2.25 2.25 0 0 0 13.5 3h-3a2.25 2.25 0 0 0-2.25 2.25v.894m7.5 0a48.667 48.667 0 0 0-7.5 0M12 12.75h.008v.008H12v-.008Z" />
                  </svg>
                </div>
                <div class="fact-meta">
                  <span class="fact-lbl">Collaboration Model</span>
                  <strong class="fact-val">Freelance & Full-time</strong>
                </div>
              </div>

              <div class="fact-tile">
                <div class="fact-icon-box">
                  <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.8" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M12 21a9.004 9.004 0 0 0 8.716-6.747M12 21a9.004 9.004 0 0 1-8.716-6.747M12 21c2.485 0 4.5-4.03 4.5-9S14.485 3 12 3m0 18c-2.485 0-4.5-4.03-4.5-9S9.515 3 12 3m0 0a8.997 8.997 0 0 1 7.843 4.582M12 3a8.997 8.997 0 0 0-7.843 4.582m15.686 0A11.953 11.953 0 0 1 12 10.5c-2.998 0-5.74-1.1-7.843-2.918m15.686 0A8.959 8.959 0 0 1 21 12c0 .778-.099 1.533-.284 2.253m0 0A17.919 17.919 0 0 1 12 16.5c-3.162 0-6.133-.815-8.716-2.247m0 0A9.015 9.015 0 0 1 3 12c0-1.605.42-3.113 1.157-4.418" />
                  </svg>
                </div>
                <div class="fact-meta">
                  <span class="fact-lbl">Primary Languages</span>
                  <strong class="fact-val">English & Persian</strong>
                </div>
              </div>

              <div class="fact-tile">
                <div class="fact-icon-box">
                  <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.8" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M4.26 10.147a60.438 60.438 0 0 0-.491 6.347A48.62 48.62 0 0 1 12 20.904a48.62 48.62 0 0 1 8.232-4.41 60.46 60.46 0 0 0-.491-6.347m-15.482 0a50.636 50.636 0 0 0-2.658-.813A59.906 59.906 0 0 1 12 3.493a59.903 59.903 0 0 1 10.399 5.84c-.896.248-1.783.52-2.658.814m-15.482 0A50.717 50.717 0 0 1 12 13.489a50.702 50.702 0 0 1 7.74-3.342M6.75 15a.75.75 0 1 0 0-1.5.75.75 0 0 0 0 1.5Zm0 0v-3.675A55.378 55.378 0 0 1 12 8.443m-7.007 11.55A5.981 5.981 0 0 0 6.75 15.75v-1.5" />
                  </svg>
                </div>
                <div class="fact-meta">
                  <span class="fact-lbl">Education Degree</span>
                  <strong class="fact-val">BSc Computer Eng. (4.5/5.0)</strong>
                </div>
              </div>
            </div>
          </div>

          <!-- Bento Card 2: Interactive Design Philosophy / Ethos -->
          <div class="bento-philosophy-card">
            <div class="bento-header">
              <span class="bento-tag">Design Ethos &amp; Beliefs</span>
              <span class="bento-hint">Interactive Principles</span>
            </div>

            <!-- Segmented Pill Selector (3 principles) -->
            <div class="ethos-tab-strip">
              <button
                v-for="(item, idx) in principles"
                :key="item.number"
                class="ethos-tab-btn"
                :class="{ 'is-active-tab': activePrinciple === idx }"
                :style="activePrinciple === idx ? {
                  borderColor: item.color,
                  background: `rgba(${item.colorRgb}, 0.14)`,
                  boxShadow: `0 4px 18px rgba(${item.colorRgb}, 0.22)`
                } : {}"
                @click="activePrinciple = idx"
              >
                <span class="ethos-tab-num" :style="{ color: item.color }">{{ item.number }}</span>
                <span class="ethos-tab-title">{{ item.title.split(' ')[0] }}</span>
              </button>
            </div>

            <!-- Focused Active Ethos Card -->
            <div
              class="ethos-active-display"
              :style="{
                borderColor: principles[activePrinciple].color,
                boxShadow: `0 8px 24px rgba(0, 0, 0, 0.35), 0 0 20px rgba(${principles[activePrinciple].colorRgb}, 0.16)`
              }"
            >
              <div class="ethos-card-header">
                <div class="ethos-title-area">
                  <div class="ethos-num-badge" :style="{ color: principles[activePrinciple].color, borderColor: `rgba(${principles[activePrinciple].colorRgb}, 0.4)` }">
                    {{ principles[activePrinciple].number }}
                  </div>
                  <div>
                    <h4 class="ethos-main-title">{{ principles[activePrinciple].title }}</h4>
                    <span class="ethos-tagline-text" :style="{ color: principles[activePrinciple].color }">{{ principles[activePrinciple].tagline }}</span>
                  </div>
                </div>
                <span class="ethos-icon-large" :style="{ color: principles[activePrinciple].color }">{{ principles[activePrinciple].icon }}</span>
              </div>

              <p class="ethos-body-desc">{{ principles[activePrinciple].desc }}</p>

              <div class="ethos-impact-row" :style="{ borderColor: `rgba(${principles[activePrinciple].colorRgb}, 0.22)`, background: `rgba(${principles[activePrinciple].colorRgb}, 0.08)` }">
                <span class="ethos-impact-star" :style="{ color: principles[activePrinciple].color }">✦</span>
                <span class="ethos-impact-label">{{ principles[activePrinciple].impact }}</span>
              </div>
            </div>
          </div>

        </div>
      </div>

    </div>
  </div>
</template>

<style scoped>
/* ─── About Me Section Wrapper ─────────────────────────── */
.aboutMe--wrapper {
  position: relative;
  padding: 100px 0;
  overflow: hidden;
}

/* Glowing purple divider line between Hero and About */
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

/* Ambient Background Glow Mesh */
.about-glow-orb {
  position: absolute;
  border-radius: 50%;
  filter: blur(110px);
  pointer-events: none;
  z-index: 0;
  opacity: 0.18;
}
.about-glow-1 {
  width: 480px;
  height: 480px;
  background: radial-gradient(circle, #6c63ff 0%, rgba(108, 99, 255, 0) 70%);
  top: 15%;
  left: -120px;
}
.about-glow-2 {
  width: 440px;
  height: 440px;
  background: radial-gradient(circle, #9b59f5 0%, rgba(155, 89, 245, 0) 70%);
  bottom: 10%;
  right: -100px;
}

.container {
  position: relative;
  z-index: 1;
}

/* Heading animation */
.aboutMe--wrapper .heading--wrapper {
  opacity: 0;
  transform: translateY(-24px);
  transition: opacity 0.8s cubic-bezier(0.22, 1, 0.36, 1), transform 0.8s cubic-bezier(0.22, 1, 0.36, 1);
  margin-bottom: 50px;
}
.active--s .heading--wrapper {
  opacity: 1;
  transform: translateY(0);
}

/* ═══════════════════════════════════════════════════════
     1. ANIMATED LIVE METRICS DASHBOARD
═══════════════════════════════════════════════════════ */
.metrics--wrapper {
  position: relative;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 16px;
  background: rgba(18, 17, 43, 0.55);
  border: 1px solid rgba(255, 255, 255, 0.08);
  border-radius: 24px;
  padding: 20px;
  margin-bottom: 75px;
  box-shadow: 0 16px 45px rgba(0, 0, 0, 0.4), 0 0 25px rgba(108, 99, 255, 0.08);
  backdrop-filter: blur(14px);
  -webkit-backdrop-filter: blur(14px);
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
  position: relative;
  display: flex;
  align-items: center;
  gap: 16px;
  padding: 16px 18px;
  background: rgba(255, 255, 255, 0.02);
  border: 1px solid rgba(255, 255, 255, 0.05);
  border-radius: 18px;
  overflow: hidden;
  min-width: 0;
  transition: all 0.35s cubic-bezier(0.25, 0.8, 0.25, 1);
  cursor: default;
}
.metric-card:hover {
  transform: translateY(-4px) scale(1.015);
}

.metric-card--indigo:hover {
  background: rgba(108, 99, 255, 0.08);
  border-color: rgba(108, 99, 255, 0.45);
  box-shadow: 0 12px 30px rgba(0, 0, 0, 0.45), 0 0 22px rgba(108, 99, 255, 0.3);
}
.metric-card--indigo .icon-box { background: rgba(108, 99, 255, 0.14); color: #818cf8; }

.metric-card--pink:hover {
  background: rgba(236, 72, 153, 0.08);
  border-color: rgba(236, 72, 153, 0.45);
  box-shadow: 0 12px 30px rgba(0, 0, 0, 0.45), 0 0 22px rgba(236, 72, 153, 0.3);
}
.metric-card--pink .icon-box { background: rgba(236, 72, 153, 0.14); color: #f472b6; }

.metric-card--emerald:hover {
  background: rgba(16, 185, 129, 0.08);
  border-color: rgba(16, 185, 129, 0.45);
  box-shadow: 0 12px 30px rgba(0, 0, 0, 0.45), 0 0 22px rgba(16, 185, 129, 0.3);
}
.metric-card--emerald .icon-box { background: rgba(16, 185, 129, 0.14); color: #34d399; }

.metric-card--amber:hover {
  background: rgba(245, 158, 11, 0.08);
  border-color: rgba(245, 158, 11, 0.45);
  box-shadow: 0 12px 30px rgba(0, 0, 0, 0.45), 0 0 22px rgba(245, 158, 11, 0.3);
}
.metric-card--amber .icon-box { background: rgba(245, 158, 11, 0.14); color: #fbbf24; }

.icon-box {
  width: 46px;
  height: 46px;
  border-radius: 13px;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
  transition: transform 0.3s ease;
}
.metric-card:hover .icon-box {
  transform: scale(1.08) rotate(4deg);
}
.m-icon { width: 22px; height: 22px; }

.m-text h3 {
  font-family: var(--font-display);
  font-size: 25px;
  color: #fff;
  margin: 0;
  font-weight: 600;
  letter-spacing: 0.3px;
  line-height: 1.1;
}
.m-text p {
  font-size: 12px;
  color: rgba(255, 255, 255, 0.6);
  margin: 2px 0 0;
  font-weight: 400;
}

/* ─── 2. Main Bento Layout ─────────────────────────────── */
.aboutContent--layout {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 36px;
  align-items: stretch;
}

/* Left & Right Stagger Animations */
.about-left {
  opacity: 0;
  transform: translateX(-40px);
  transition: opacity 0.85s 0.15s cubic-bezier(0.22, 1, 0.36, 1), transform 0.85s 0.15s cubic-bezier(0.22, 1, 0.36, 1);
  display: flex;
  flex-direction: column;
  gap: 24px;
}
.active--s .about-left {
  opacity: 1;
  transform: translateX(0);
}

.about-right {
  opacity: 0;
  transform: translateX(40px);
  transition: opacity 0.85s 0.25s cubic-bezier(0.22, 1, 0.36, 1), transform 0.85s 0.25s cubic-bezier(0.22, 1, 0.36, 1);
  display: flex;
  flex-direction: column;
  gap: 24px;
}
.active--s .about-right {
  opacity: 1;
  transform: translateX(0);
}

/* ─── Profile Master Card (Left Top) ───────────────────── */
.avatar-card-modern {
  display: flex;
  align-items: center;
  gap: 20px;
  background: rgba(15, 13, 36, 0.85);
  border: 1px solid rgba(255, 255, 255, 0.12);
  border-radius: 22px;
  padding: 22px 26px;
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
  box-shadow: 0 14px 40px rgba(0, 0, 0, 0.4), 0 0 25px rgba(108, 99, 255, 0.08);
  transition: all 0.3s ease;
}
.avatar-card-modern:hover {
  border-color: rgba(155, 89, 245, 0.4);
  box-shadow: 0 16px 45px rgba(0, 0, 0, 0.5), 0 0 30px rgba(108, 99, 255, 0.2);
  transform: translateY(-2px);
}

.avatar-ring-box {
  position: relative;
  width: 72px;
  height: 72px;
  flex-shrink: 0;
}
.avatar-ring-glow {
  position: absolute;
  inset: -3px;
  border-radius: 50%;
  background: linear-gradient(135deg, #6c63ff 0%, #9b59f5 50%, #34d399 100%);
  animation: spinGlow 8s linear infinite;
  filter: blur(2px);
}
@keyframes spinGlow {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}

.avatar-photo {
  position: relative;
  width: 100%;
  height: 100%;
  border-radius: 50%;
  object-fit: cover;
  border: 3px solid #0c0a20;
  z-index: 1;
}
.avatar-initials {
  position: relative;
  width: 100%;
  height: 100%;
  border-radius: 50%;
  background: #1e1b4b;
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: var(--font-display);
  font-size: 24px;
  font-weight: 600;
  color: #fff;
  border: 3px solid #0c0a20;
  z-index: 1;
}

.avatar-info-modern {
  display: flex;
  flex-direction: column;
  gap: 4px;
  flex: 1;
}
.avatar-header-row {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 10px;
  flex-wrap: wrap;
}
.avatar-name {
  font-family: var(--font-display);
  font-size: 19px;
  font-weight: 600;
  color: #fff;
  margin: 0;
  letter-spacing: 0.5px;
}

.live-status-pill {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  font-size: 11px;
  font-weight: 500;
  color: #34d399;
  background: rgba(52, 211, 153, 0.1);
  border: 1px solid rgba(52, 211, 153, 0.3);
  padding: 3px 10px;
  border-radius: 20px;
}
.pulse-beacon {
  width: 6px;
  height: 6px;
  border-radius: 50%;
  background: #34d399;
  box-shadow: 0 0 8px #34d399;
  animation: beaconPulse 2s infinite;
}

.avatar-title-tag {
  font-size: 13px;
  color: rgba(255, 255, 255, 0.65);
  margin: 0;
  font-weight: 500;
}

.avatar-badges-row {
  display: flex;
  gap: 8px;
  margin-top: 4px;
  flex-wrap: wrap;
}
.badge-mini {
  font-size: 11px;
  color: rgba(255, 255, 255, 0.5);
  background: rgba(255, 255, 255, 0.04);
  padding: 2px 8px;
  border-radius: 6px;
  border: 1px solid rgba(255, 255, 255, 0.06);
}

/* ─── Story Block (Left Bottom) ────────────────────────── */
.story-block-modern {
  background: rgba(15, 13, 36, 0.85);
  border: 1px solid rgba(255, 255, 255, 0.12);
  border-radius: 22px;
  padding: 28px;
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
  box-shadow: 0 14px 40px rgba(0, 0, 0, 0.4), 0 0 25px rgba(108, 99, 255, 0.08);
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  flex: 1;
  transition: border-color 0.3s ease, box-shadow 0.3s ease;
}
.story-block-modern:hover {
  border-color: rgba(155, 89, 245, 0.35);
  box-shadow: 0 14px 40px rgba(0, 0, 0, 0.45), 0 0 28px rgba(108, 99, 255, 0.12);
}

.story-title-modern {
  display: flex;
  flex-direction: column;
  margin-bottom: 16px;
  line-height: 1.25;
}
.story-sub {
  font-size: 18px;
  font-weight: 400;
  color: rgba(255, 255, 255, 0.7);
}
.story-highlight {
  font-family: var(--font-display);
  font-size: clamp(22px, 2.5vw, 30px);
  font-weight: 600;
  letter-spacing: 0.3px;
  background: linear-gradient(135deg, #ffffff 30%, #a78bfa 70%, #6c63ff 100%);
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
}

.story-text {
  font-size: 14.5px;
  color: rgba(255, 255, 255, 0.68);
  line-height: 1.75;
  margin-bottom: 14px;
}
.story-text strong {
  color: #fff;
  font-weight: 600;
}
.story-text em {
  color: rgba(255, 255, 255, 0.95);
  font-style: italic;
}

/* CTA Row */
.cta-row-modern {
  display: flex;
  align-items: center;
  gap: 14px;
  flex-wrap: wrap;
  margin-top: auto;
  padding-top: 10px;
}
.btn-icon { width: 17px; height: 17px; }

/* ─── Right Bento Column ───────────────────────────────── */
.bento-facts-card, .bento-philosophy-card {
  background: rgba(15, 13, 36, 0.85);
  border: 1px solid rgba(255, 255, 255, 0.12);
  border-radius: 22px;
  padding: 24px 26px;
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
  box-shadow: 0 14px 40px rgba(0, 0, 0, 0.4), 0 0 25px rgba(108, 99, 255, 0.08);
  transition: border-color 0.3s ease;
}
.bento-philosophy-card {
  flex: 1;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}
.bento-facts-card:hover, .bento-philosophy-card:hover {
  border-color: rgba(155, 89, 245, 0.35);
}

.bento-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 18px;
}
.bento-tag {
  font-size: 11px;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 1px;
  color: rgba(255, 255, 255, 0.45);
}
.bento-hint {
  font-size: 10.5px;
  color: #a78bfa;
  font-family: monospace;
}
.bento-dot-indicator {
  width: 6px;
  height: 6px;
  border-radius: 50%;
  background: #6c63ff;
  box-shadow: 0 0 8px #6c63ff;
}

/* Facts Grid */
.facts-grid-modern {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 16px;
}
.fact-tile {
  display: flex;
  align-items: center;
  gap: 12px;
  background: rgba(255, 255, 255, 0.03);
  border: 1px solid rgba(255, 255, 255, 0.06);
  padding: 12px 14px;
  border-radius: 14px;
  transition: all 0.25s ease;
}
.fact-tile:hover {
  background: rgba(108, 99, 255, 0.1);
  border-color: rgba(108, 99, 255, 0.3);
  transform: translateY(-2px);
}
.fact-icon-box {
  width: 36px;
  height: 36px;
  border-radius: 10px;
  background: rgba(108, 99, 255, 0.15);
  color: #a78bfa;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
}
.fact-icon-box svg { width: 18px; height: 18px; }
.fact-meta { display: flex; flex-direction: column; }
.fact-lbl { font-size: 11px; color: rgba(255, 255, 255, 0.45); margin-bottom: 2px; }
.fact-val { font-size: 13px; color: #fff; font-weight: 600; }

/* ─── Philosophy Interactive Segmented Showcase ──────── */
.ethos-tab-strip {
  display: flex;
  gap: 8px;
  margin-bottom: 16px;
}
.ethos-tab-btn {
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 6px;
  padding: 10px 14px;
  border-radius: 12px;
  background: rgba(255, 255, 255, 0.04);
  border: 1px solid rgba(255, 255, 255, 0.08);
  cursor: pointer;
  transition: all 0.25s ease;
  color: rgba(255, 255, 255, 0.7);
  min-height: 42px;
}
.ethos-tab-btn:hover {
  background: rgba(255, 255, 255, 0.08);
  border-color: rgba(255, 255, 255, 0.16);
  color: #fff;
  transform: translateY(-1px);
}
.ethos-tab-btn.is-active-tab {
  color: #fff;
  transform: translateY(-2px);
}
.ethos-tab-num {
  font-size: 11.5px;
  font-weight: 700;
  font-family: monospace;
}
.ethos-tab-title {
  font-size: 13px;
  font-weight: 600;
  letter-spacing: 0.2px;
}

/* Focused Active Ethos Card */
.ethos-active-display {
  background: rgba(18, 15, 42, 0.75);
  border: 1.5px solid;
  border-radius: 18px;
  padding: 22px 24px;
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
  transition: all 0.35s cubic-bezier(0.22, 1, 0.36, 1);
  animation: ethosFadeIn 0.35s ease;
}
@keyframes ethosFadeIn {
  from { opacity: 0; transform: translateY(6px); }
  to { opacity: 1; transform: translateY(0); }
}

.ethos-card-header {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  gap: 14px;
  margin-bottom: 12px;
}
.ethos-title-area {
  display: flex;
  align-items: center;
  gap: 12px;
}
.ethos-num-badge {
  font-size: 12px;
  font-weight: 700;
  font-family: monospace;
  padding: 3px 8px;
  border-radius: 8px;
  border: 1px solid;
  background: rgba(0, 0, 0, 0.35);
  flex-shrink: 0;
}
.ethos-main-title {
  font-family: var(--font-display);
  font-size: 17px;
  font-weight: 600;
  color: #fff;
  margin: 0 0 3px;
  letter-spacing: 0.3px;
}
.ethos-tagline-text {
  font-size: 12px;
  font-weight: 500;
  display: block;
}
.ethos-icon-large {
  font-size: 22px;
  line-height: 1;
  flex-shrink: 0;
}

.ethos-body-desc {
  font-size: 13px;
  color: rgba(255, 255, 255, 0.68);
  line-height: 1.65;
  margin: 0 0 16px;
}

.ethos-impact-row {
  display: flex;
  align-items: center;
  gap: 8px;
  padding: 8px 14px;
  border-radius: 10px;
  border: 1px solid;
}
.ethos-impact-star {
  font-size: 12px;
  flex-shrink: 0;
}
.ethos-impact-label {
  font-size: 12px;
  font-weight: 500;
  color: rgba(255, 255, 255, 0.9);
}

/* ─── Responsive Media Queries ───────────────────────── */
@media screen and (max-width: 1120px) {
  .metrics--wrapper {
    grid-template-columns: repeat(2, 1fr);
    gap: 14px;
    padding: 18px;
  }
  .aboutContent--layout {
    grid-template-columns: 1fr;
    gap: 28px;
  }
}

@media screen and (max-width: 768px) {
  .aboutMe--wrapper {
    padding: 64px 0;
  }
  .about-left, .about-right {
    transform: translateY(20px);
  }
  .active--s .about-left, .active--s .about-right {
    transform: translateY(0);
  }
  .metrics--wrapper {
    grid-template-columns: 1fr;
    gap: 12px;
    padding: 14px;
    margin-bottom: 45px;
  }
  .metric-card {
    padding: 12px 14px;
    gap: 12px;
  }
  .icon-box {
    width: 40px;
    height: 40px;
  }
  .m-icon {
    width: 20px;
    height: 20px;
  }
  .m-text h3 {
    font-size: 22px;
  }
  .m-text p {
    font-size: 11.5px;
  }

  /* Profile Card Mobile Stack (Centered Column) */
  .avatar-card-modern {
    flex-direction: column;
    text-align: center;
    padding: 20px;
  }
  .avatar-ring-box {
    width: 72px;
    height: 72px;
  }
  .avatar-header-row {
    justify-content: center;
  }
  .avatar-badges-row {
    justify-content: center;
  }

  /* Story block */
  .story-block-modern {
    padding: 20px 18px;
  }
  .story-sub {
    font-size: 13px;
  }
  .story-highlight {
    font-size: 20px;
    line-height: 1.25;
  }
  .story-text {
    font-size: 13.5px;
    line-height: 1.6;
    margin-bottom: 12px;
  }

  /* Facts Grid Mobile Stack (1fr on top of each other) */
  .facts-grid-modern {
    grid-template-columns: 1fr;
    gap: 12px;
  }

  /* Ethos Mobile Standard (Clean uncollapsed layout) */
  .ethos-tab-btn {
    padding: 8px 6px;
    min-height: 38px;
  }
  .ethos-tab-title {
    font-size: 11.5px;
  }
  .ethos-active-display {
    padding: 16px;
  }
  .ethos-card-header {
    display: flex;
    align-items: flex-start;
    justify-content: space-between;
    gap: 12px;
    margin-bottom: 12px;
  }
  .ethos-num-badge {
    display: none !important;
  }
  .ethos-title-area {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    gap: 4px;
    flex: 1;
    min-width: 0;
  }
  .ethos-main-title {
    font-size: 16px;
    font-weight: 600;
    line-height: 1.35;
    margin: 0;
  }
  .ethos-tagline-text {
    font-size: 12px;
    font-weight: 500;
    line-height: 1.4;
  }
  .ethos-icon-large {
    font-size: 20px;
    line-height: 1;
    flex-shrink: 0;
    margin-top: 2px;
  }
  .ethos-body-desc {
    font-size: 12.5px;
    line-height: 1.55;
    margin-bottom: 12px;
  }
  .ethos-impact-row {
    padding: 7px 10px;
  }
  .ethos-impact-label {
    font-size: 11.5px;
  }

  .cta-row-modern {
    flex-direction: column;
    width: 100%;
    gap: 10px;
  }
  .cta-row-modern .cta-btn {
    width: 100%;
    justify-content: center;
    padding: 14px 20px;
  }
}

@media screen and (max-width: 480px) {
  .metrics--wrapper {
    grid-template-columns: 1fr;
  }
  .story-block-modern, .bento-facts-card, .bento-philosophy-card {
    padding: 18px;
  }
  .story-highlight {
    font-size: 22px;
  }
}
</style>