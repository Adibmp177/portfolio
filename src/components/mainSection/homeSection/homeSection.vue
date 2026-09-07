<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue';

// ── Role typing animation sequence ────────────────────────
const roles = [
  'UI/UX Designer',
  'Product Thinker',
  'Interaction Designer',
  'Visual Storyteller',
  'Design Systems Lead',
  'Problem Solver',
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
      const pauseDuration = roleIndex === 0 ? 3500 : 2000;
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

  const speed = isDeleting ? 45 : 75;
  typingTimer = setTimeout(typeEffect, speed);
}

// ── Interactive Design System Workbench State ─────────────
const activeTab = ref('all'); // 'all' | 'tokens' | 'components'

// 1. Color Tokens & Theme System Map
const activeColor = ref('#6C63FF');
const swatches = [
  { 
    name: 'Primary', 
    hex: '#6C63FF', 
    code: '#6C63FF', 
    bg: 'linear-gradient(135deg, #6C63FF 0%, #9B59F5 100%)' 
  },
  { 
    name: 'Pink', 
    hex: '#EC4899', 
    code: '#EC4899', 
    bg: '#EC4899' 
  },
  { 
    name: 'Emerald', 
    hex: '#10B981', 
    code: '#10B981', 
    bg: '#10B981' 
  },
  { 
    name: 'Amber', 
    hex: '#F59E0B', 
    code: '#F59E0B', 
    bg: '#F59E0B' 
  },
];

const themeMap = {
  '#6C63FF': { start: '#6C63FF', end: '#9B59F5', rgb: '108, 99, 255', glow: 'rgba(108, 99, 255, 0.45)', hoverGlow: 'rgba(108, 99, 255, 0.7)' },
  '#EC4899': { start: '#EC4899', end: '#F472B6', rgb: '236, 72, 153', glow: 'rgba(236, 72, 153, 0.45)', hoverGlow: 'rgba(236, 72, 153, 0.7)' },
  '#10B981': { start: '#10B981', end: '#34D399', rgb: '16, 185, 129', glow: 'rgba(16, 185, 129, 0.45)', hoverGlow: 'rgba(16, 185, 129, 0.7)' },
  '#F59E0B': { start: '#F59E0B', end: '#FBBF24', rgb: '245, 158, 11', glow: 'rgba(245, 158, 11, 0.45)', hoverGlow: 'rgba(245, 158, 11, 0.7)' },
};

const currentTheme = computed(() => themeMap[activeColor.value] || themeMap['#6C63FF']);

function selectSwatch(hex) {
  activeColor.value = hex;
}

// 2. Elevation & Depth Token State (Subtle, professional glassmorphic depth levels)
const activeElevation = ref('Elevated');
const elevationTokens = [
  { label: 'Flat', val: 'Flat' },
  { label: 'Elevated', val: 'Elevated' },
  { label: 'Ambient Float', val: 'Ambient Float' }
];

// 3. Typography Token State
const activeFontSize = ref('14px');
const fontTokens = [
  { label: 'Display', size: '18px' },
  { label: 'Heading', size: '15px' },
  { label: 'Body', size: '13px' }
];

// 4. Component Variant State
const activeVariant = ref('Default');
const variants = ['Default', 'Hover', 'Focus', 'Disabled'];

// 5. Component Live Controls
const isToggleActive = ref(true);
function toggleSwitch() {
  isToggleActive.value = !isToggleActive.value;
}

const searchQuery = ref('');
const isInputFocused = ref(false);

// 6. Interactive Motion & Easing Playground State
const activeEase = ref('Spring'); // 'Linear' | 'Ease' | 'Spring'
const motionDuration = ref('3.2s');

const easingCurves = {
  Linear: {
    name: 'Linear',
    path: 'M 10 32 L 210 6',
    bezier: 'linear'
  },
  Ease: {
    name: 'Ease-Out',
    path: 'M 10 32 C 60 32 50 6 210 6',
    bezier: 'cubic-bezier(0.25, 1, 0.5, 1)'
  },
  Spring: {
    name: 'Spring Bounce',
    path: 'M 10 32 C 60 32 80 2 130 18 C 170 30 190 6 210 6',
    bezier: 'cubic-bezier(0.34, 1.56, 0.64, 1)'
  }
};

const currentEase = computed(() => easingCurves[activeEase.value] || easingCurves['Spring']);

onMounted(() => {
  typingTimer = setTimeout(typeEffect, 600);
});

onUnmounted(() => {
  if (typingTimer) clearTimeout(typingTimer);
});
</script>

<template>
  <div class="hero-split-container container">
    <!-- Desktop-Only Ambient Pattern & Glow Mesh (Seamless radial fade, no rectangle borders) -->
    <div class="hero-desktop-mesh">
      <div class="hero-dot-pattern"></div>
      <div class="hero-name-glow"></div>
    </div>

    <div class="hero-grid">
      <!-- LEFT COLUMN: Brand Identity & Typography -->
      <div class="hero-left">
        <!-- Mobile Glowing Ambient Circle Positioned Behind Name & Role -->
        <div class="hero-mobile-glow"></div>

        <!-- Greeting & Headline -->
        <p class="greeting">Hi, I'm</p>
        <h1 class="myName">Adib Mohammadpouri</h1>

        <!-- Dynamic Subtitle -->
        <div class="subtitle">
          <span class="static-txt">Specializing in</span>
          <span class="role-badge">
            {{ displayedRole }}<span class="cursor">|</span>
          </span>
        </div>

        <!-- Description -->
        <p class="intro">
          I design clean, purposeful digital interfaces & systems. Turning complex ideas into intuitive products people enjoy using, and businesses love to scale with.
        </p>

        <!-- CTA Buttons -->
        <div class="homeButton--wrapper">
          <a href="#Portfolio" class="cta-btn cta-btn--primary" id="hero-view-projects-btn">
            <svg class="btn-icon" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <polygon points="12 2 2 7 12 12 22 7 12 2"></polygon>
              <polyline points="2 17 12 22 22 17"></polyline>
              <polyline points="2 12 12 17 22 12"></polyline>
            </svg>
            <span class="btn-label">View My Projects</span>
          </a>

          <a href="#contact" class="cta-btn cta-btn--outline" id="hero-contact-btn">
            <svg class="btn-icon" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <path d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07 19.5 19.5 0 0 1-6-6 19.79 19.79 0 0 1-3.07-8.67A2 2 0 0 1 4.11 2h3a2 2 0 0 1 2 1.72 12.84 12.84 0 0 0 .7 2.81 2 2 0 0 1-.45 2.11L8.09 9.91a16 16 0 0 0 6 6l1.27-1.27a2 2 0 0 1 2.11-.45 12.84 12.84 0 0 0 2.81.7A2 2 0 0 1 22 16.92z"></path>
            </svg>
            <span class="btn-label">Contact Me</span>
          </a>
        </div>

        <!-- Social Connections -->
        <div class="social--wrapper">
          <span class="social-label">Connect:</span>
          <!-- Figma -->
          <a href="https://www.figma.com/@adibmohammadpou" class="social-icon" aria-label="Figma" target="_blank" rel="noopener noreferrer" title="Figma">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 38 57" fill="currentColor">
              <path d="M19 28.5a9.5 9.5 0 1 1 19 0 9.5 9.5 0 0 1-19 0Z"/>
              <path d="M0 47.5A9.5 9.5 0 0 1 9.5 38H19v9.5a9.5 9.5 0 0 1-19 0Z"/>
              <path d="M19 0v19h9.5a9.5 9.5 0 0 0 0-19H19Z"/>
              <path d="M0 9.5A9.5 9.5 0 0 0 9.5 19H19V0H9.5A9.5 9.5 0 0 0 0 9.5Z"/>
              <path d="M0 28.5A9.5 9.5 0 0 0 9.5 38H19V19H9.5A9.5 9.5 0 0 0 0 28.5Z"/>
            </svg>
          </a>
          <!-- LinkedIn -->
          <a href="https://www.linkedin.com/in/adibmohammadpouri/" class="social-icon" aria-label="LinkedIn" target="_blank" rel="noopener noreferrer" title="LinkedIn">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor">
              <path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433a2.062 2.062 0 0 1-2.063-2.065 2.064 2.064 0 1 1 2.063 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/>
            </svg>
          </a>
          <!-- Telegram -->
          <a href="https://t.me/Adibmohamadpori" class="social-icon" aria-label="Telegram" target="_blank" rel="noopener noreferrer" title="Telegram">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor">
              <path d="M12 0C5.373 0 0 5.373 0 12s5.373 12 12 12 12-5.373 12-12S18.627 0 12 0Zm5.562 8.248-2.04 9.617c-.152.672-.554.836-1.123.52l-3.1-2.285-1.495 1.438c-.165.165-.304.304-.624.304l.223-3.167 5.754-5.195c.25-.223-.054-.347-.388-.124L7.29 14.806l-3.045-.953c-.663-.207-.677-.663.138-.98l11.893-4.585c.551-.199 1.033.134.857.98l-.571-.02Z"/>
            </svg>
          </a>
          <!-- Dribbble -->
          <a href="https://dribbble.com/adibmohammadpouri" class="social-icon" aria-label="Dribbble" target="_blank" rel="noopener noreferrer" title="Dribbble">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor">
              <path d="M12 2a10 10 0 1 0 10 10A10.011 10.011 0 0 0 12 2zm6.75 6.09a8.02 8.02 0 0 1 2.06 5.25c-.32-.05-3.83-.56-7.38-.07a41.87 41.87 0 0 0-.74-1.52c3.55-1.41 5.04-3.1 5.17-3.25a7.9 7.9 0 0 1 .89-.41zm-1.82-.77c-.12.14-1.49 1.7-4.85 3.01a45.69 45.69 0 0 0-3.3-4.94A8.07 8.07 0 0 1 12 4a7.94 7.94 0 0 1 4.93 1.32zM8.34 2.8a44.62 44.62 0 0 1 3.23 4.88c-3.79 1.05-7.14 1.04-7.5 1.04a7.99 7.99 0 0 1 4.27-5.92zm-5.18 7.4c.39 0 3.38.01 7.02-.97.26.51.51 1.03.75 1.55-3.84 1.09-7.34 1.57-7.69 1.62a8.04 8.04 0 0 1-.08-2.2zm1.2 3.81c.32-.04 3.49-.49 7.15-1.53.86 2.37 1.37 4.74 1.54 5.67A8.02 8.02 0 0 1 4.36 14.01zm9.4 6.8c-.18-.97-.66-3.28-1.5-5.59 3.3-.43 6.55.03 6.87.08a8.02 8.02 0 0 1-5.37 5.51z"/>
            </svg>
          </a>
        </div>
      </div>

      <!-- RIGHT COLUMN: Design System Studio Window -->
      <div class="hero-right">
        <div class="figma-window">
          <!-- Window Header Controls -->
          <div class="window-header">
            <div class="window-controls">
              <span class="dot dot-red"></span>
              <span class="dot dot-yellow"></span>
              <span class="dot dot-green"></span>
            </div>
            <div class="file-tab">
              <svg class="figma-logo-mini" viewBox="0 0 38 57" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path d="M19 28.5a9.5 9.5 0 1 1 19 0 9.5 9.5 0 0 1-19 0Z" fill="#1ABCFE"/>
                <path d="M0 47.5A9.5 9.5 0 0 1 9.5 38H19v9.5a9.5 9.5 0 0 1-19 0Z" fill="#0ACF83"/>
                <path d="M19 0v19h9.5a9.5 9.5 0 0 0 0-19H19Z" fill="#FF7262"/>
                <path d="M0 9.5A9.5 9.5 0 0 0 9.5 19H19V0H9.5A9.5 9.5 0 0 0 0 9.5Z" fill="#F24E1E"/>
                <path d="M0 28.5A9.5 9.5 0 0 0 9.5 38H19V19H9.5A9.5 9.5 0 0 0 0 28.5Z" fill="#A259FF"/>
              </svg>
              <span>core-design-system.fig</span>
            </div>
            <div class="canvas-status">
              <span class="status-dot-green"></span> Studio Active
            </div>
          </div>

          <!-- Canvas Viewport -->
          <div class="canvas-viewport">
            <div class="figma-artboard">
              <!-- Interactive Tab Navigation -->
              <div class="artboard-tabs">
                <button 
                  class="tab-btn" 
                  :class="{ active: activeTab === 'all' }"
                  :style="activeTab === 'all' ? { borderColor: currentTheme.start, background: `rgba(${currentTheme.rgb}, 0.18)`, color: '#ffffff', boxShadow: `0 2px 10px rgba(${currentTheme.rgb}, 0.2)` } : {}"
                  @click="activeTab = 'all'"
                >
                  All Overview
                </button>
                <button 
                  class="tab-btn" 
                  :class="{ active: activeTab === 'tokens' }"
                  :style="activeTab === 'tokens' ? { borderColor: currentTheme.start, background: `rgba(${currentTheme.rgb}, 0.18)`, color: '#ffffff', boxShadow: `0 2px 10px rgba(${currentTheme.rgb}, 0.2)` } : {}"
                  @click="activeTab = 'tokens'"
                >
                  Tokens
                </button>
                <button 
                  class="tab-btn" 
                  :class="{ active: activeTab === 'components' }"
                  :style="activeTab === 'components' ? { borderColor: currentTheme.start, background: `rgba(${currentTheme.rgb}, 0.18)`, color: '#ffffff', boxShadow: `0 2px 10px rgba(${currentTheme.rgb}, 0.2)` } : {}"
                  @click="activeTab = 'components'"
                >
                  Components
                </button>
              </div>

              <!-- Animated Designer Cursor Tag -->
              <div class="designer-cursor-tag">
                <svg class="cursor-arrow" viewBox="0 0 24 24" :fill="currentTheme.start" xmlns="http://www.w3.org/2000/svg">
                  <path d="M5.5 3.2L18.7 12L12.4 13.9L8.7 20.8L5.5 3.2Z" stroke="#ffffff" stroke-width="1.5"/>
                </svg>
                <span class="tag-name" :style="{ background: currentTheme.start, boxShadow: `0 3px 10px rgba(${currentTheme.rgb}, 0.5)` }">Adib (Managing System)</span>
              </div>

              <!-- FIXED-HEIGHT Workbench Container -->
              <div class="ui-workbench-card">
                <!-- ════════════════════════════════════════════════
                     SECTION 1: COLOR TOKENS (Full Width Symmetrical Palette)
                ════════════════════════════════════════════════ -->
                <div class="workbench-section" v-if="activeTab === 'all' || activeTab === 'tokens'">
                  <div class="section-header">
                    <span class="section-lbl">Brand Color Tokens</span>
                    <span class="token-count" :style="{ color: currentTheme.start }">Active: {{ activeColor }}</span>
                  </div>
                  <div class="color-swatches">
                    <div 
                      class="swatch-item" 
                      v-for="swatch in swatches" 
                      :key="swatch.hex"
                      @click="selectSwatch(swatch.hex)"
                    >
                      <div 
                        class="swatch" 
                        :style="{ background: swatch.bg || swatch.hex, boxShadow: activeColor === swatch.hex ? `0 0 16px ${currentTheme.glow}` : 'none' }"
                        :class="{ 'swatch-active': activeColor === swatch.hex }"
                      ></div>
                      <span class="swatch-code">{{ swatch.code || swatch.hex }}</span>
                    </div>
                  </div>
                </div>

                <!-- TYPOGRAPHY TOKENS (Tokens tab) -->
                <div class="workbench-section token-sub-section" v-if="activeTab === 'tokens'">
                  <div class="section-header">
                    <span class="section-lbl">Typography Tokens</span>
                    <span class="token-count" :style="{ color: currentTheme.start }">Scale: {{ activeFontSize }}</span>
                  </div>
                  <div class="font-scale-selector">
                    <button 
                      class="font-token-pill" 
                      v-for="font in fontTokens" 
                      :key="font.label"
                      :class="{ active: activeFontSize === font.size }"
                      :style="activeFontSize === font.size ? {
                        borderColor: currentTheme.start,
                        background: `rgba(${currentTheme.rgb}, 0.18)`,
                        color: '#ffffff',
                        boxShadow: `0 4px 14px rgba(${currentTheme.rgb}, 0.25)`
                      } : {}"
                      @click="activeFontSize = font.size"
                    >
                      {{ font.label }}
                    </button>
                  </div>
                  <div class="typography-live-preview" :style="{ fontSize: activeFontSize }">
                    <span :style="{ color: currentTheme.start }">The quick brown fox</span> jumps over design limits.
                  </div>
                </div>

                <!-- ELEVATION & DEPTH TOKENS (Tokens tab - Live Interactive Surface) -->
                <div class="workbench-section token-sub-section" v-if="activeTab === 'tokens'">
                  <div class="section-header">
                    <span class="section-lbl">Elevation & Depth Tokens</span>
                    <span class="token-count" :style="{ color: currentTheme.start }">Level: {{ activeElevation }}</span>
                  </div>
                  <div class="elevation-selector">
                    <button 
                      class="elevation-pill" 
                      v-for="e in elevationTokens" 
                      :key="e.val"
                      :class="{ active: activeElevation === e.val }"
                      :style="activeElevation === e.val ? {
                        borderColor: currentTheme.start,
                        background: `rgba(${currentTheme.rgb}, 0.18)`,
                        color: '#ffffff',
                        boxShadow: `0 4px 14px rgba(${currentTheme.rgb}, 0.28)`
                      } : {}"
                      @click="activeElevation = e.val"
                    >
                      {{ e.label }}
                    </button>
                  </div>
                  <div 
                    class="elevation-live-preview"
                    :style="{
                      boxShadow: activeElevation === 'Flat'
                        ? '0 2px 6px rgba(0, 0, 0, 0.35)'
                        : activeElevation === 'Elevated'
                        ? `0 8px 24px rgba(0, 0, 0, 0.5), 0 0 14px rgba(${currentTheme.rgb}, 0.25)`
                        : `0 14px 34px rgba(0, 0, 0, 0.6), 0 0 22px rgba(${currentTheme.rgb}, 0.40), 0 0 45px rgba(${currentTheme.rgb}, 0.15)`,
                      borderColor: activeElevation === 'Ambient Float' 
                        ? currentTheme.start 
                        : activeElevation === 'Elevated'
                        ? `rgba(${currentTheme.rgb}, 0.45)`
                        : 'rgba(255, 255, 255, 0.10)',
                      background: activeElevation === 'Ambient Float'
                        ? `rgba(${currentTheme.rgb}, 0.12)`
                        : activeElevation === 'Elevated'
                        ? `rgba(${currentTheme.rgb}, 0.05)`
                        : 'rgba(255, 255, 255, 0.02)',
                      transform: activeElevation === 'Flat' ? 'none' : activeElevation === 'Elevated' ? 'translateY(-2px)' : 'translateY(-3px)'
                    }"
                  >
                    <div class="preview-inner-content">
                      <span class="preview-indicator" :style="{ background: currentTheme.start, color: currentTheme.start, boxShadow: `0 0 10px ${currentTheme.start}` }"></span>
                      <span>Live Surface Preview: <strong>{{ activeElevation }} Depth</strong></span>
                    </div>
                  </div>
                </div>

                <!-- ════════════════════════════════════════════════
                     SECTION 2: UI COMPONENTS
                ════════════════════════════════════════════════ -->
                <div class="workbench-section" v-if="activeTab === 'all' || activeTab === 'components'">
                  <div class="section-header">
                    <span class="section-lbl">UI Component Library</span>
                    <span class="token-count" :style="{ color: currentTheme.start }">Variant: {{ activeVariant }}</span>
                  </div>
                  <div class="component-preview">
                    <!-- Dynamic Button -->
                    <button 
                      class="sample-btn"
                      :class="[`state-${activeVariant.toLowerCase()}`]"
                      :style="{ 
                        background: activeVariant === 'Disabled' 
                          ? 'rgba(255, 255, 255, 0.12)' 
                          : activeVariant === 'Hover'
                          ? `linear-gradient(135deg, ${currentTheme.end} 0%, ${currentTheme.start} 100%)`
                          : `linear-gradient(135deg, ${currentTheme.start} 0%, ${currentTheme.end} 100%)`, 
                        borderRadius: '12px',
                        boxShadow: activeVariant === 'Disabled'
                          ? 'none'
                          : activeVariant === 'Focus'
                          ? `0 0 0 2px #0c0a20, 0 0 0 4px ${currentTheme.start}, 0 0 16px ${currentTheme.glow}`
                          : activeVariant === 'Hover'
                          ? `0 8px 24px ${currentTheme.hoverGlow}`
                          : `0 4px 14px ${currentTheme.glow}`,
                        transform: activeVariant === 'Hover' ? 'translateY(-2px) scale(1.04)' : activeVariant === 'Focus' ? 'scale(1.02)' : 'none',
                        opacity: activeVariant === 'Disabled' ? '0.45' : '1',
                        cursor: activeVariant === 'Disabled' ? 'not-allowed' : 'pointer'
                      }"
                    >
                      <svg class="btn-sparkle" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                        <path d="M12 2L15 9L22 12L15 15L12 22L9 15L2 12L9 9L12 2Z"/>
                      </svg>
                      <span>Explore UI</span>
                    </button>

                    <!-- Controls Row: Search Input on Left, Toggle Switch on Right -->
                    <div class="component-controls-row">
                      <!-- Search Input -->
                      <div 
                        class="sample-input" 
                        :style="{ 
                          borderRadius: '12px',
                          borderColor: isInputFocused ? currentTheme.start : 'rgba(255, 255, 255, 0.1)',
                          boxShadow: isInputFocused ? `0 0 12px ${currentTheme.glow}` : 'none'
                        }"
                      >
                        <svg class="search-icon" :style="{ color: isInputFocused ? currentTheme.start : 'rgba(255, 255, 255, 0.4)' }" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                          <circle cx="11" cy="11" r="8"></circle>
                          <line x1="21" y1="21" x2="16.65" y2="16.65"></line>
                        </svg>
                        <input 
                          type="text" 
                          v-model="searchQuery" 
                          placeholder="Type..."
                          class="interactive-input-field"
                          @focus="isInputFocused = true"
                          @blur="isInputFocused = false"
                        />
                      </div>

                      <!-- Smooth Spring Animated Toggle Switch -->
                      <div 
                        class="sample-toggle" 
                        :class="{ 'toggle-on': isToggleActive }"
                        :style="{
                          background: isToggleActive 
                            ? `linear-gradient(90deg, ${currentTheme.start} 0%, ${currentTheme.end} 100%)` 
                            : 'rgba(255, 255, 255, 0.12)',
                          boxShadow: isToggleActive ? `0 0 12px ${currentTheme.glow}` : 'none'
                        }"
                        @click="toggleSwitch"
                      >
                        <span class="toggle-knob"></span>
                      </div>
                    </div>
                  </div>
                </div>

                <!-- VARIANT MATRIX (Components tab - Clean labels without redundant 'State' text) -->
                <div class="workbench-section token-sub-section" v-if="activeTab === 'components'">
                  <div class="section-header">
                    <span class="section-lbl">Component State Matrix</span>
                    <span class="token-count" :style="{ color: currentTheme.start }">Active: {{ activeVariant }}</span>
                  </div>
                  <div class="variant-matrix-chips">
                    <button 
                      class="variant-chip" 
                      v-for="v in variants" 
                      :key="v"
                      :class="{ active: activeVariant === v }"
                      :style="activeVariant === v ? {
                        borderColor: currentTheme.start,
                        background: `rgba(${currentTheme.rgb}, 0.18)`,
                        color: '#ffffff',
                        boxShadow: `0 4px 14px rgba(${currentTheme.rgb}, 0.25)`
                      } : {}"
                      @click="activeVariant = v"
                    >
                      {{ v }}
                    </button>
                  </div>
                </div>

                <!-- ════════════════════════════════════════════════
                     SECTION 3: INTERACTIVE MOTION & EASING PLAYGROUND
                ════════════════════════════════════════════════ -->
                <div class="workbench-section animation-section" v-if="activeTab === 'all' || activeTab === 'components'">
                  <div class="section-header">
                    <span class="section-lbl">Motion & Easing Curves</span>
                    <span class="ease-val" :style="{ color: currentTheme.start }">{{ currentEase.bezier }} ({{ motionDuration }})</span>
                  </div>

                  <!-- Interactive Curve Formula Selector Buttons -->
                  <div class="motion-curve-selectors">
                    <button 
                      class="ease-chip" 
                      v-for="(curve, key) in easingCurves" 
                      :key="key"
                      :class="{ active: activeEase === key }"
                      :style="activeEase === key ? {
                        borderColor: currentTheme.start,
                        background: `rgba(${currentTheme.rgb}, 0.18)`,
                        color: '#ffffff',
                        boxShadow: `0 4px 14px rgba(${currentTheme.rgb}, 0.25)`
                      } : {}"
                      @click="activeEase = key"
                    >
                      {{ curve.name }}
                    </button>
                  </div>

                  <!-- Live Path-Following SVG Curve Visualizer -->
                  <div class="curve-box" title="Watch circle move along path curve">
                    <svg viewBox="0 0 220 38" class="curve-svg">
                      <!-- Curve Path Line -->
                      <path 
                        :d="currentEase.path" 
                        fill="none" 
                        :stroke="currentTheme.start" 
                        stroke-width="3" 
                        stroke-linecap="round"
                        class="animated-stroke-line"
                      />
                      <!-- Live Smooth Path-Following Ball (Locks onto path & glides gently at 3.2s) -->
                      <circle 
                        r="5" 
                        :fill="currentTheme.end" 
                        class="live-moving-dot"
                        :style="{
                          offsetPath: `path('${currentEase.path}')`,
                          WebkitOffsetPath: `path('${currentEase.path}')`,
                          animationDuration: motionDuration
                        }"
                      />
                    </svg>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <!-- 3 Floating Specialty Badges (With project-matching hover animations) -->
          <div class="floating-badge float-top-right">
            <span class="badge-emoji">🎨</span>
            <div class="badge-info">
              <strong>Figma Master</strong>
              <span>Design Systems</span>
            </div>
          </div>

          <div class="floating-badge float-bottom-left">
            <span class="badge-emoji">📱</span>
            <div class="badge-info">
              <strong>Responsive UI</strong>
              <span>Web & Mobile</span>
            </div>
          </div>

          <div class="floating-badge float-bottom-right">
            <span class="badge-emoji">⚡</span>
            <div class="badge-info">
              <strong>Prototyping</strong>
              <span>Interactive Motion</span>
            </div>
          </div>

        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
/* ─── Hero Main Container ─────────────────────────────── */
.hero-split-container {
  position: relative;
  width: 100%;
  margin: 0 auto;
  box-sizing: border-box;
}

/* ─── Desktop-Only Ambient Pattern & Lighting Mesh ───── */
.hero-desktop-mesh {
  position: absolute;
  inset: -80px -60px;
  pointer-events: none;
  z-index: 0;
}

.hero-dot-pattern {
  position: absolute;
  inset: 0;
  background-image: radial-gradient(rgba(255, 255, 255, 0.08) 1.2px, transparent 1.2px);
  background-size: 32px 32px;
  mask-image: radial-gradient(ellipse 75% 65% at 48% 45%, rgba(0, 0, 0, 0.85) 0%, rgba(0, 0, 0, 0.35) 45%, transparent 75%);
  -webkit-mask-image: radial-gradient(ellipse 75% 65% at 48% 45%, rgba(0, 0, 0, 0.85) 0%, rgba(0, 0, 0, 0.35) 45%, transparent 75%);
}

.hero-name-glow {
  position: absolute;
  top: 40px;
  left: -20px;
  width: 620px;
  height: 480px;
  border-radius: 50%;
  background: radial-gradient(circle, rgba(108, 99, 255, 0.16) 0%, rgba(155, 89, 245, 0.07) 50%, transparent 70%);
  filter: blur(80px);
}

@media screen and (max-width: 991px) {
  .hero-desktop-mesh {
    display: none !important;
  }
}

/* ─── Grid Layout ─────────────────────────────────────── */
.hero-grid {
  position: relative;
  z-index: 1;
  display: grid;
  grid-template-columns: 1.15fr 0.85fr;
  gap: clamp(24px, 3.5vw, 44px);
  align-items: center;
  width: 100%;
  box-sizing: border-box;
}

/* ─── Left Column Styling ─────────────────────────────── */
.hero-left {
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  text-align: left;
}

/* Mobile Glowing Ambient Circle Positioned Behind Name & Role */
.hero-mobile-glow {
  display: none;
}
@media screen and (max-width: 991px) {
  .hero-mobile-glow {
    display: block;
    position: absolute;
    top: -40px;
    left: 50%;
    transform: translateX(-50%);
    width: 520px;
    height: 420px;
    border-radius: 50%;
    background: radial-gradient(ellipse 65% 55% at 50% 50%, rgba(108, 99, 255, 0.14) 0%, rgba(155, 89, 245, 0.05) 55%, transparent 72%);
    filter: blur(65px);
    pointer-events: none;
    z-index: 0;
  }
}

/* Greeting & Name */
.greeting {
  font-size: 16px;
  font-weight: 400;
  color: rgba(255, 255, 255, 0.6);
  letter-spacing: 0.5px;
  margin-bottom: 8px;
  opacity: 0;
  transform: translateY(16px);
  transition: opacity 0.7s 0.15s ease-out, transform 0.7s 0.15s ease-out;
}
.active--s .greeting { opacity: 1; transform: translateY(0); }

.myName {
  font-family: var(--font-display);
  font-size: clamp(34px, 4.4vw, 60px);
  font-weight: 700;
  line-height: 1.08;
  letter-spacing: -0.5px;
  background: linear-gradient(135deg, #ffffff 40%, #a78bfa 75%, #6c63ff 100%);
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
  margin-bottom: 16px;
  opacity: 0;
  transform: translateY(20px);
  transition: opacity 0.8s 0.2s ease-out, transform 0.8s 0.2s ease-out;
  overflow-wrap: break-word;
  word-break: normal;
}
.active--s .myName { opacity: 1; transform: translateY(0); }

/* Subtitle & Role */
.subtitle {
  font-size: 18px;
  font-weight: 400;
  color: rgba(255, 255, 255, 0.75);
  display: flex;
  align-items: center;
  gap: 8px;
  margin-bottom: 20px;
  opacity: 0;
  transform: translateY(18px);
  transition: opacity 0.8s 0.3s ease-out, transform 0.8s 0.3s ease-out;
}
.active--s .subtitle { opacity: 1; transform: translateY(0); }

.static-txt { color: rgba(255, 255, 255, 0.55); }
.role-badge {
  font-weight: 600;
  background: linear-gradient(90deg, #6c63ff 0%, #9b59f5 100%);
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
}

.cursor {
  color: #9b59f5;
  font-weight: 300;
  animation: blink 1s step-end infinite;
}
@keyframes blink { 0%, 100% { opacity: 1; } 50% { opacity: 0; } }

/* Intro text */
.intro {
  font-size: 15.5px;
  line-height: 1.75;
  color: rgba(255, 255, 255, 0.6);
  max-width: 520px;
  margin-bottom: 32px;
  opacity: 0;
  transform: translateY(20px);
  transition: opacity 0.8s 0.4s ease-out, transform 0.8s 0.4s ease-out;
}
.active--s .intro { opacity: 1; transform: translateY(0); }

/* Buttons */
.homeButton--wrapper {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  gap: 16px;
  margin-bottom: 32px;
  opacity: 0;
  transform: translateY(20px);
  transition: opacity 0.8s 0.5s ease-out, transform 0.8s 0.5s ease-out;
}
.active--s .homeButton--wrapper { opacity: 1; transform: translateY(0); }

.cta-btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
  padding: 14px 28px;
  border-radius: 50px;
  font-size: 15px;
  font-weight: 500;
  letter-spacing: 0.2px;
  cursor: pointer;
  text-decoration: none;
  transition: all 0.3s cubic-bezier(0.25, 0.8, 0.25, 1);
}

.btn-icon {
  width: 18px;
  height: 18px;
  flex-shrink: 0;
  transition: transform 0.3s ease;
}

.cta-btn--primary {
  color: #fff;
  background: linear-gradient(90deg, #6c63ff 0%, #9b59f5 50%, #6c63ff 100%);
  background-size: 200% 100%;
  box-shadow: 0 4px 24px rgba(108, 99, 255, 0.42);
}
.cta-btn--primary:hover {
  background-position: right center;
  box-shadow: 0 8px 32px rgba(155, 89, 245, 0.6);
  transform: translateY(-3px);
}
.cta-btn--primary:hover .btn-icon { transform: translateY(-2px) scale(1.1); }

.cta-btn--outline {
  color: #ffffff;
  background: rgba(255, 255, 255, 0.04);
  border: 1px solid rgba(255, 255, 255, 0.15);
  backdrop-filter: blur(10px);
}
.cta-btn--outline:hover {
  background: rgba(108, 99, 255, 0.15);
  border-color: rgba(155, 89, 245, 0.5);
  box-shadow: 0 6px 24px rgba(108, 99, 255, 0.2);
  transform: translateY(-3px);
}

/* Social Row */
.social--wrapper {
  display: flex;
  align-items: center;
  gap: 14px;
  opacity: 0;
  transform: translateY(16px);
  transition: opacity 0.8s 0.6s ease-out, transform 0.8s 0.6s ease-out;
}
.active--s .social--wrapper { opacity: 1; transform: translateY(0); }

.social-label {
  font-size: 13px;
  color: rgba(255, 255, 255, 0.45);
  font-weight: 500;
}

.social-icon {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 42px;
  height: 42px;
  border-radius: 50%;
  color: rgba(255, 255, 255, 0.6);
  border: 1px solid rgba(255, 255, 255, 0.1);
  background: rgba(255, 255, 255, 0.03);
  backdrop-filter: blur(8px);
  transition: all 0.25s ease;
}
.social-icon svg { width: 18px; height: 18px; }
.social-icon:hover {
  color: #fff;
  border-color: rgba(155, 89, 245, 0.6);
  background: rgba(108, 99, 255, 0.2);
  box-shadow: 0 6px 20px rgba(108, 99, 255, 0.35);
  transform: translateY(-3px);
}

/* ─── Right Column Figma Live Showcase Window (Flat Clean 2D) ── */
.hero-right {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 20px 10px;
  opacity: 0;
  transform: translateY(24px);
  transition: opacity 0.9s 0.3s ease-out, transform 0.9s 0.3s ease-out;
}
.active--s .hero-right { opacity: 1; transform: translateY(0); }

.figma-window {
  position: relative;
  width: 100%;
  max-width: 450px;
  border-radius: 20px;
  background: rgba(12, 10, 32, 0.88);
  border: 1px solid rgba(255, 255, 255, 0.12);
  backdrop-filter: blur(24px);
  -webkit-backdrop-filter: blur(24px);
  box-shadow:
    0 25px 60px rgba(0, 0, 0, 0.65),
    0 0 40px rgba(108, 99, 255, 0.15);
  padding: 16px;
  overflow: visible;
}

/* Window Top Control Bar */
.window-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding-bottom: 12px;
  border-bottom: 1px solid rgba(255, 255, 255, 0.08);
  margin-bottom: 14px;
}
.window-controls {
  display: flex;
  gap: 6px;
}
.dot { width: 10px; height: 10px; border-radius: 50%; }
.dot-red { background: #ff5f56; }
.dot-yellow { background: #ffbd2e; }
.dot-green { background: #27c93f; }

.file-tab {
  display: flex;
  align-items: center;
  gap: 6px;
  font-size: 12px;
  font-weight: 500;
  color: rgba(255, 255, 255, 0.75);
  padding: 4px 10px;
  border-radius: 8px;
  background: rgba(255, 255, 255, 0.05);
}
.figma-logo-mini { width: 12px; height: 18px; }
.canvas-status {
  display: flex;
  align-items: center;
  gap: 5px;
  font-size: 11px;
  color: rgba(255, 255, 255, 0.5);
}
.status-dot-green {
  width: 6px;
  height: 6px;
  border-radius: 50%;
  background: #10b981;
  box-shadow: 0 0 8px #10b981;
}

/* Canvas Viewport */
.canvas-viewport {
  position: relative;
  padding: 4px 2px;
}

/* Figma Frame Container */
.figma-artboard {
  position: relative;
  border: 1.5px dashed rgba(108, 99, 255, 0.45);
  border-radius: 16px;
  padding: 16px 14px;
  background: rgba(255, 255, 255, 0.02);
}

/* Artboard Filter Tabs */
.artboard-tabs {
  display: flex;
  gap: 6px;
  margin-bottom: 12px;
}
.tab-btn {
  font-size: 10.5px;
  font-weight: 500;
  color: rgba(255, 255, 255, 0.5);
  background: rgba(255, 255, 255, 0.03);
  border: 1px solid rgba(255, 255, 255, 0.08);
  padding: 4px 11px;
  border-radius: 12px;
  cursor: pointer;
  transition: all 0.2s ease;
}
.tab-btn.active, .tab-btn:hover {
  color: #fff;
  background: rgba(108, 99, 255, 0.2);
  border-color: rgba(155, 89, 245, 0.4);
}

/* Designer Live Cursor Tag */
.designer-cursor-tag {
  position: absolute;
  top: -14px;
  right: 18px;
  display: flex;
  align-items: center;
  gap: 4px;
  z-index: 10;
  animation: cursorFloat 3.5s ease-in-out infinite alternate;
}

@keyframes cursorFloat {
  0% { transform: translate(0, 0); }
  100% { transform: translate(-6px, 8px); }
}

.cursor-arrow {
  width: 16px;
  height: 16px;
  filter: drop-shadow(0 2px 4px rgba(0,0,0,0.5));
}
.tag-name {
  font-size: 10.5px;
  font-weight: 600;
  color: #fff;
  background: #9b59f5;
  padding: 2px 8px;
  border-radius: 10px;
  box-shadow: 0 3px 10px rgba(155, 89, 245, 0.5);
  white-space: nowrap;
}

/* ── FIXED HEIGHT WORKBENCH CONTAINER ────────────────── */
.ui-workbench-card {
  display: flex;
  flex-direction: column;
  gap: 14px;
  height: 310px;
  overflow-y: auto;
  background: linear-gradient(145deg, rgba(255, 255, 255, 0.04) 0%, rgba(255, 255, 255, 0.01) 100%);
  border: 1px solid rgba(255, 255, 255, 0.08);
  border-radius: 14px;
  padding: 14px;
  box-sizing: border-box;
}

.ui-workbench-card::-webkit-scrollbar {
  width: 4px;
}
.ui-workbench-card::-webkit-scrollbar-thumb {
  background: rgba(108, 99, 255, 0.3);
  border-radius: 10px;
}

.workbench-section {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.section-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.section-lbl {
  font-size: 11px;
  font-weight: 600;
  color: rgba(255, 255, 255, 0.6);
  letter-spacing: 0.2px;
}

.token-count {
  font-size: 10px;
  font-weight: 500;
  color: #a78bfa;
  font-family: monospace;
}

/* 1. Color Swatches - Full Width Grid */
.color-swatches {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 10px;
  width: 100%;
}
.swatch-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 5px;
  width: 100%;
  cursor: pointer;
}
.swatch {
  width: 100%;
  height: 32px;
  border-radius: 9px;
  border: 1.5px solid rgba(255, 255, 255, 0.15);
  transition: all 0.25s cubic-bezier(0.25, 0.8, 0.25, 1);
}
.swatch-item:hover .swatch, .swatch-active {
  transform: translateY(-2px);
  border-color: #fff;
}

.swatch-code {
  font-size: 10px;
  color: rgba(255, 255, 255, 0.6);
  font-family: monospace;
  font-weight: 500;
}

/* Typography Token Sub-Section */
.font-scale-selector {
  display: flex;
  gap: 6px;
}
.font-token-pill {
  font-size: 10.5px;
  font-weight: 500;
  color: rgba(255, 255, 255, 0.6);
  background: rgba(255, 255, 255, 0.04);
  border: 1px solid rgba(255, 255, 255, 0.1);
  padding: 4px 10px;
  border-radius: 8px;
  cursor: pointer;
  transition: all 0.2s ease;
}
.font-token-pill.active, .font-token-pill:hover {
  color: #fff;
  background: rgba(108, 99, 255, 0.2);
  border-color: #9b59f5;
}
.typography-live-preview {
  color: rgba(255, 255, 255, 0.8);
  font-weight: 500;
  transition: font-size 0.25s ease;
  line-height: 1.3;
  margin-top: 4px;
}

/* Elevation & Depth Token Sub-Section */
.elevation-selector {
  display: flex;
  align-items: stretch;
  gap: 6px;
  width: 100%;
}
.elevation-pill {
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  font-size: 11px;
  font-weight: 500;
  color: rgba(255, 255, 255, 0.6);
  background: rgba(255, 255, 255, 0.04);
  border: 1px solid rgba(255, 255, 255, 0.1);
  padding: 6px 6px;
  min-height: 42px;
  border-radius: 8px;
  cursor: pointer;
  line-height: 1.25;
  transition: all 0.2s ease;
  box-sizing: border-box;
}
.elevation-pill.active, .elevation-pill:hover {
  color: #fff;
  background: rgba(108, 99, 255, 0.2);
  border-color: #9b59f5;
}

.elevation-live-preview {
  margin-top: 6px;
  padding: 10px 12px;
  border-radius: 10px;
  background: rgba(255, 255, 255, 0.04);
  border: 1px solid rgba(255, 255, 255, 0.12);
  transition: all 0.3s cubic-bezier(0.25, 0.8, 0.25, 1);
}

.preview-inner-content {
  display: flex;
  align-items: center;
  gap: 8px;
  font-size: 11px;
  color: rgba(255, 255, 255, 0.85);
}

.preview-indicator {
  width: 8px;
  height: 8px;
  border-radius: 50%;
  box-shadow: 0 0 8px currentColor;
}

/* Variant State Matrix Sub-Section */
.variant-matrix-chips {
  display: flex;
  gap: 6px;
  flex-wrap: wrap;
}
.variant-chip {
  font-size: 10.5px;
  font-weight: 500;
  color: rgba(255, 255, 255, 0.6);
  background: rgba(255, 255, 255, 0.04);
  border: 1px solid rgba(255, 255, 255, 0.1);
  padding: 4px 10px;
  border-radius: 8px;
  cursor: pointer;
  transition: all 0.2s ease;
}
.variant-chip.active, .variant-chip:hover {
  color: #fff;
  background: rgba(155, 89, 245, 0.25);
  border-color: #9b59f5;
}

/* 2. Component System Sample */
.component-preview {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 8px;
  background: rgba(108, 99, 255, 0.06);
  border: 1px solid rgba(108, 99, 255, 0.18);
  border-radius: 12px;
  padding: 10px;
  transition: all 0.25s ease;
}

.sample-btn {
  display: flex;
  align-items: center;
  gap: 6px;
  font-size: 11px;
  font-weight: 600;
  color: #fff;
  border: none;
  outline: none;
  padding: 6px 14px;
  border-radius: 12px;
  transition: all 0.25s cubic-bezier(0.25, 0.8, 0.25, 1);
  user-select: none;
}
.sample-btn:hover {
  transform: translateY(-2px) scale(1.04) !important;
}
.sample-btn:active {
  transform: translateY(0) scale(0.97) !important;
}
.btn-sparkle { width: 12px; height: 12px; transition: transform 0.25s ease; }
.sample-btn:hover .btn-sparkle { transform: rotate(15deg) scale(1.1); }

.component-controls-row {
  display: contents;
}

.sample-input {
  display: flex;
  align-items: center;
  gap: 6px;
  background: rgba(255, 255, 255, 0.04);
  border: 1px solid rgba(255, 255, 255, 0.1);
  padding: 5px 9px;
  border-radius: 12px;
  flex: 1;
  max-width: 115px;
  transition: all 0.25s ease;
}
.search-icon { width: 12px; height: 12px; flex-shrink: 0; transition: color 0.25s ease; }
.interactive-input-field {
  width: 100%;
  background: transparent;
  border: none;
  outline: none;
  color: #fff;
  font-size: 11px;
  font-family: var(--font-body);
}
.interactive-input-field::placeholder { color: rgba(255, 255, 255, 0.35); }

/* ── SMOOTH SPRING ANIMATED TOGGLE SWITCH ─────────────── */
.sample-toggle {
  position: relative;
  width: 38px;
  height: 20px;
  border-radius: 20px;
  background: rgba(255, 255, 255, 0.12);
  padding: 2px;
  cursor: pointer;
  transition: background 0.3s ease, box-shadow 0.3s ease;
  user-select: none;
}
.toggle-knob {
  position: absolute;
  top: 2px;
  left: 2px;
  width: 16px;
  height: 16px;
  border-radius: 50%;
  background: #fff;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.4);
  transition: transform 0.35s cubic-bezier(0.34, 1.56, 0.64, 1);
}
.sample-toggle.toggle-on .toggle-knob {
  transform: translateX(18px);
}

/* ── INTERACTIVE MOTION PLAYGROUND ────────────────────── */
.motion-curve-selectors {
  display: flex;
  align-items: stretch;
  gap: 6px;
  margin-top: 2px;
  width: 100%;
}
.ease-chip {
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  font-size: 10.5px;
  font-weight: 500;
  color: rgba(255, 255, 255, 0.6);
  background: rgba(255, 255, 255, 0.04);
  border: 1px solid rgba(255, 255, 255, 0.1);
  padding: 6px 6px;
  min-height: 42px;
  border-radius: 8px;
  cursor: pointer;
  line-height: 1.25;
  transition: all 0.2s ease;
  box-sizing: border-box;
}
.ease-chip.active, .ease-chip:hover {
  color: #fff;
  background: rgba(108, 99, 255, 0.2);
  border-color: #9b59f5;
}

.ease-val {
  font-size: 10px;
  color: #a78bfa;
  font-weight: 500;
  font-family: monospace;
}

.curve-box {
  width: 100%;
  height: 34px;
  margin-top: 4px;
  cursor: pointer;
}
.curve-svg {
  width: 100%;
  height: 100%;
  overflow: visible;
}
.animated-stroke-line {
  transition: stroke 0.35s ease, d 0.35s ease;
}

/* Live Path-Following Ball along SVG Curve */
.live-moving-dot {
  transition: fill 0.35s ease;
  animation: moveAlongPath 3.2s ease-in-out infinite alternate;
}

@keyframes moveAlongPath {
  0% {
    offset-distance: 0%;
    -webkit-offset-distance: 0%;
  }
  100% {
    offset-distance: 100%;
    -webkit-offset-distance: 100%;
  }
}

/* ─── Floating Specialty Badges (With Project-Matching Hover Effect) ─── */
.floating-badge {
  position: absolute;
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 9px 16px;
  border-radius: 14px;
  background: rgba(15, 12, 38, 0.95);
  border: 1px solid rgba(255, 255, 255, 0.15);
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
  box-shadow: 0 12px 30px rgba(0, 0, 0, 0.55);
  z-index: 20;
  cursor: pointer;
  transition: color 0.28s ease, border-color 0.28s ease, background 0.28s ease, box-shadow 0.28s ease, transform 0.28s cubic-bezier(0.25, 0.8, 0.25, 1);
  animation: badgeFloat 4s ease-in-out infinite alternate;
}

.floating-badge:hover {
  border-color: rgba(155, 89, 245, 0.6);
  background: rgba(108, 99, 255, 0.22);
  box-shadow: 0 8px 25px rgba(108, 99, 255, 0.38);
  transform: translateY(-5px) scale(1.04);
}

@keyframes badgeFloat {
  0% { transform: translateY(0); }
  100% { transform: translateY(-7px); }
}

/* Position Coordinates - Zero Overlap */
.float-top-right {
  top: -24px;
  right: -24px;
}

.float-bottom-left {
  bottom: -24px;
  left: -24px;
  animation-delay: -1.8s;
}

.float-bottom-right {
  bottom: -24px;
  right: -24px;
  animation-delay: -3s;
}

.badge-emoji { font-size: 17px; }
.badge-info {
  display: flex;
  flex-direction: column;
  text-align: left;
}
.badge-info strong {
  font-size: 12.5px;
  color: #fff;
  font-weight: 600;
  line-height: 1.2;
}
.badge-info span {
  font-size: 10px;
  color: rgba(255, 255, 255, 0.5);
}

/* ─── Responsive Media Queries (Mobile First UX & Touch Guidelines) ──── */
@media screen and (max-width: 1250px) {
  .float-top-right {
    top: -16px;
    right: -8px;
    transform: scale(0.92);
  }
  .float-bottom-left {
    bottom: -16px;
    left: -8px;
    transform: scale(0.92);
  }
  .float-bottom-right {
    display: none;
  }
}

@media screen and (max-width: 1100px) {
  .hero-grid {
    grid-template-columns: 1.1fr 0.9fr;
    gap: 24px;
  }
  .myName {
    font-size: clamp(32px, 3.8vw, 48px);
  }
  .figma-window {
    max-width: 410px;
  }
  .float-top-right {
    top: -12px;
    right: 0px;
    transform: scale(0.85);
  }
  .float-bottom-left {
    bottom: -12px;
    left: 0px;
    transform: scale(0.85);
  }
  .float-bottom-right { display: none; }
}

@media screen and (max-width: 991px) {
  .hero-split-container {
    padding-top: 0;
    padding-bottom: 0;
  }
  .hero-grid {
    grid-template-columns: 1fr;
    gap: 36px;
  }
  .hero-left {
    align-items: center;
    text-align: center;
  }
  .subtitle { justify-content: center; }
  .intro { max-width: 95%; }
  .floating-badge { display: none; } /* Hide floating badges on touch screens to maximize canvas space */
  
  .figma-window {
    max-width: 100%;
    padding: 14px;
  }
}

@media screen and (max-width: 768px) {
  .hero-split-container {
    padding-top: 0;
    padding-bottom: 0;
  }

  .greeting {
    font-size: 15px;
  }

  .myName {
    font-size: clamp(32px, 8vw, 46px);
    line-height: 1.12;
    margin-bottom: 12px;
  }

  .subtitle {
    font-size: 16px;
    flex-wrap: wrap;
    margin-bottom: 16px;
  }

  .intro {
    font-size: 14.5px;
    line-height: 1.65;
    margin-bottom: 24px;
  }

  .homeButton--wrapper {
    flex-direction: column;
    width: 100%;
    gap: 12px;
    margin-bottom: 24px;
  }

  .cta-btn {
    width: 100%;
    padding: 14px 20px;
    font-size: 14.5px;
    box-sizing: border-box;
  }

  /* ── Mobile Window Header Optimization (Prevent Collapsing) ── */
  .canvas-status {
    display: none !important;
  }
  .file-tab {
    white-space: nowrap;
    font-size: 11px;
    padding: 3px 8px;
    gap: 5px;
  }
  .file-tab span {
    white-space: nowrap;
  }
  .window-header {
    padding-bottom: 10px;
    margin-bottom: 12px;
  }

  /* ── Mobile Workbench Touch Controls (44px Minimum Touch Target Standards) ── */
  .figma-artboard {
    padding: 12px 10px;
  }

  .artboard-tabs {
    gap: 6px;
    justify-content: space-between;
  }

  .tab-btn {
    flex: 1;
    font-size: 11.5px;
    font-weight: 600;
    padding: 8px 10px;
    min-height: 36px;
    text-align: center;
    border-radius: 10px;
  }

  .designer-cursor-tag {
    top: -10px;
    right: 8px;
    transform: scale(0.85);
  }

  .ui-workbench-card {
    height: 345px;
    padding: 12px;
    gap: 14px;
  }

  /* Color Swatches Touch Optimization (Full width grid on mobile too) */
  .color-swatches {
    gap: 8px;
  }

  .swatch {
    height: 34px;
    border-radius: 8px;
  }

  .swatch-code {
    font-size: 10px;
    font-weight: 500;
  }

  /* Typography & Elevation Token Pills - Unified Equal Height */
  .font-scale-selector, .elevation-selector {
    display: flex;
    align-items: stretch;
    gap: 6px;
    width: 100%;
  }

  .font-token-pill {
    flex: 1;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 6px 8px;
    font-size: 11.5px;
    min-height: 44px;
    text-align: center;
    box-sizing: border-box;
  }

  .elevation-pill {
    flex: 1;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 6px 6px;
    font-size: 11px;
    line-height: 1.25;
    min-height: 44px;
    text-align: center;
    box-sizing: border-box;
  }

  /* Component Library Sample Rows (Row 1: Button Fill; Row 2: Search Left + Toggle Right) */
  .component-preview {
    display: flex;
    flex-direction: column;
    gap: 8px;
    padding: 10px;
  }

  .sample-btn {
    width: 100% !important;
    min-height: 36px;
    padding: 8px 14px;
    font-size: 11.5px;
    justify-content: center;
    box-sizing: border-box;
  }

  .component-controls-row {
    display: flex !important;
    flex-direction: row !important;
    align-items: center !important;
    gap: 8px;
    width: 100% !important;
    box-sizing: border-box;
  }

  .sample-input {
    flex: 1 1 0% !important;
    min-width: 0 !important;
    max-width: none !important;
    min-height: 36px;
    padding: 6px 10px;
    box-sizing: border-box;
  }

  .interactive-input-field {
    width: 100% !important;
    min-width: 0 !important;
    font-size: 11px;
  }

  .sample-toggle {
    flex-shrink: 0 !important;
    width: 42px;
    height: 22px;
    padding: 2px;
    box-sizing: border-box;
  }

  .toggle-knob {
    width: 18px;
    height: 18px;
  }

  .sample-toggle.toggle-on .toggle-knob {
    transform: translateX(20px);
  }

  /* Matrix Chips & Motion Chips - Unified Equal Height */
  .variant-matrix-chips, .motion-curve-selectors {
    display: flex;
    align-items: stretch;
    gap: 6px;
    width: 100%;
  }

  .variant-chip {
    flex: 1;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 6px 8px;
    font-size: 11px;
    min-height: 40px;
    text-align: center;
    box-sizing: border-box;
  }

  .ease-chip {
    flex: 1;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 6px 6px;
    font-size: 11px;
    line-height: 1.25;
    min-height: 44px;
    text-align: center;
    box-sizing: border-box;
  }
}

@media screen and (max-width: 480px) {
  .hero-split-container {
    padding-top: 0;
    padding-bottom: 0;
  }

  .myName {
    font-size: 28px;
  }

  .figma-window {
    padding: 10px;
    border-radius: 16px;
  }

  .tab-btn {
    font-size: 10.5px;
    padding: 7px 6px;
  }

  .ui-workbench-card {
    height: 340px;
    padding: 10px;
  }
}
</style>