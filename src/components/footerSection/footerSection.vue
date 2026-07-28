<script setup>
const year = new Date().getFullYear();

const navLinks = [
    { label: 'Home', href: '#home' },
    { label: 'About Me', href: '#aboutMe' },
    { label: 'Services', href: '#services' },
    { label: 'Portfolio', href: '#Portfolio' },
    { label: 'Contact', href: '#contact' },
];

const socials = [
    {
        label: 'Figma',
        href: 'https://www.figma.com/@adibmohammadpou',
        icon: `<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 38 57" fill="currentColor"><path d="M19 28.5a9.5 9.5 0 1 1 19 0 9.5 9.5 0 0 1-19 0Z"/><path d="M0 47.5A9.5 9.5 0 0 1 9.5 38H19v9.5a9.5 9.5 0 0 1-19 0Z"/><path d="M19 0v19h9.5a9.5 9.5 0 0 0 0-19H19Z"/><path d="M0 9.5A9.5 9.5 0 0 0 9.5 19H19V0H9.5A9.5 9.5 0 0 0 0 9.5Z"/><path d="M0 28.5A9.5 9.5 0 0 0 9.5 38H19V19H9.5A9.5 9.5 0 0 0 0 28.5Z"/></svg>`
    },
    {
        label: 'LinkedIn',
        href: 'https://www.linkedin.com/in/adibmohammadpouri/',
        icon: `<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor"><path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433a2.062 2.062 0 0 1-2.063-2.065 2.064 2.064 0 1 1 2.063 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/></svg>`
    },
    {
        label: 'Telegram',
        href: 'https://t.me/Adibmohamadpori',
        icon: `<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor"><path d="M12 0C5.373 0 0 5.373 0 12s5.373 12 12 12 12-5.373 12-12S18.627 0 12 0Zm5.562 8.248-2.04 9.617c-.152.672-.554.836-1.123.52l-3.1-2.285-1.495 1.438c-.165.165-.304.304-.624.304l.223-3.167 5.754-5.195c.25-.223-.054-.347-.388-.124L7.29 14.806l-3.045-.953c-.663-.207-.677-.663.138-.98l11.893-4.585c.551-.199 1.033.134.857.98l-.571-.02Z"/></svg>`
    },
    {
        label: 'Dribbble',
        href: 'https://dribbble.com/adibmohammadpouri',
        icon: `<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor"><path d="M12 2a10 10 0 1 0 10 10A10.011 10.011 0 0 0 12 2zm6.75 6.09a8.02 8.02 0 0 1 2.06 5.25c-.32-.05-3.83-.56-7.38-.07a41.87 41.87 0 0 0-.74-1.52c3.55-1.41 5.04-3.1 5.17-3.25a7.9 7.9 0 0 1 .89-.41zm-1.82-.77c-.12.14-1.49 1.7-4.85 3.01a45.69 45.69 0 0 0-3.3-4.94A8.07 8.07 0 0 1 12 4a7.94 7.94 0 0 1 4.93 1.32zM8.34 2.8a44.62 44.62 0 0 1 3.23 4.88c-3.79 1.05-7.14 1.04-7.5 1.04a7.99 7.99 0 0 1 4.27-5.92zm-5.18 7.4c.39 0 3.38.01 7.02-.97.26.51.51 1.03.75 1.55-3.84 1.09-7.34 1.57-7.69 1.62a8.04 8.04 0 0 1-.08-2.2zm1.2 3.81c.32-.04 3.49-.49 7.15-1.53.86 2.37 1.37 4.74 1.54 5.67A8.02 8.02 0 0 1 4.36 14.01zm9.4 6.8c-.18-.97-.66-3.28-1.5-5.59 3.3-.43 6.55.03 6.87.08a8.02 8.02 0 0 1-5.37 5.51z"/></svg>`
    }
];
</script>

<template>
    <footer class="footer">
        <div class="footer-glow"></div>
        <div class="container footer-inner">

            <!-- Left: Brand -->
            <div class="footer-brand">
                <a href="#home" class="brand-logo">
                    <img src="/logo/LOGO.png" alt="Adib Logo" class="footer-logo-img" />
                </a>
                <p class="brand-tagline">Crafting high-converting digital products &amp; intuitive user interfaces that turn visitors into customers.</p>
                <div class="footer-socials">
                    <a
                        v-for="social in socials"
                        :key="social.label"
                        :href="social.href"
                        target="_blank"
                        :aria-label="social.label"
                        class="footer-social-icon"
                        v-html="social.icon"
                    ></a>
                </div>
            </div>

            <!-- Center: Navigation -->
            <div class="footer-nav">
                <p class="footer-section-label">Navigation</p>
                <ul class="footer-links">
                    <li v-for="link in navLinks" :key="link.label">
                        <a :href="link.href" class="footer-link">
                            <span class="link-arrow">→</span>
                            {{ link.label }}
                        </a>
                    </li>
                </ul>
            </div>

            <!-- Right: CTA -->
            <div class="footer-cta">
                <p class="footer-section-label">Let's Work Together</p>
                <p class="footer-cta-text">Have a project in mind? I'd love to hear about it and build something great.</p>
                <a href="#contact" class="cta-btn cta-btn--primary footer-cta-btn" id="footer-contact-btn">
                    Get in Touch
                </a>
                <div class="footer-available">
                    <span class="available-dot"></span>
                    <span>Currently available for projects</span>
                </div>
            </div>

        </div>

        <!-- Bottom Bar -->
        <div class="footer-bottom">
            <div class="container footer-bottom-inner">
                <p class="footer-copy">© {{ year }} Adib Mohammad Pouri. All rights reserved.</p>
                <a href="#home" class="back-to-top-btn" aria-label="Back to top">
                    <span>Back to top</span>
                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M4.5 15.75l7.5-7.5 7.5 7.5" />
                    </svg>
                </a>
                <p class="footer-made">Designed &amp; Developed with ♥</p>
            </div>
        </div>
    </footer>
</template>

<style scoped>
.footer {
    position: relative;
    border-top: 1px solid rgba(108, 99, 255, 0.15);
    overflow: hidden;
    margin-top: 0;
    background:
        linear-gradient(180deg, rgba(8, 7, 20, 0.0) 0%, rgba(6, 5, 16, 0.85) 100%),
        radial-gradient(ellipse 60% 40% at 50% 0%, rgba(108, 99, 255, 0.08) 0%, transparent 70%);
}

.footer-glow {
    position: absolute;
    top: 0;
    left: 50%;
    transform: translateX(-50%);
    width: 55%;
    height: 1px;
    background: linear-gradient(90deg, transparent, rgba(108, 99, 255, 0.9), rgba(155, 89, 245, 0.9), transparent);
    filter: blur(0.5px);
}

/* Separator from contact section */
.footer::before {
    content: '';
    display: block;
    height: 1px;
    background: linear-gradient(90deg, transparent 0%, rgba(108, 99, 255, 0.25) 30%, rgba(155, 89, 245, 0.25) 70%, transparent 100%);
    margin-bottom: 0;
}

.footer-inner {
    display: flex;
    gap: 48px;
    padding-top: 56px;
    padding-bottom: 48px;
    justify-content: space-between;
    flex-wrap: wrap;
}

/* ── Brand ── */
.footer-brand {
    flex: 1.2;
    min-width: 220px;
}
.brand-logo {
    display: inline-block;
    margin-bottom: 16px;
}
.footer-logo-img {
    height: 50px;
    width: auto;
    object-fit: contain;
    display: block;
}
.brand-tagline {
    font-size: 14px;
    color: rgba(255, 255, 255, 0.6);
    line-height: 1.65;
    margin-bottom: 22px;
    max-width: 280px;
}
.footer-socials {
    display: flex;
    gap: 10px;
}
.footer-social-icon {
    width: 38px;
    height: 38px;
    border-radius: 10px;
    background: rgba(255, 255, 255, 0.04);
    border: 1px solid rgba(255, 255, 255, 0.08);
    color: rgba(255, 255, 255, 0.5);
    display: flex;
    align-items: center;
    justify-content: center;
    transition: background 0.25s ease, border-color 0.25s ease, color 0.25s ease, transform 0.25s ease;
    text-decoration: none;
}
.footer-social-icon :deep(svg) {
    width: 16px;
    height: 16px;
}
.footer-social-icon:hover {
    background: rgba(108, 99, 255, 0.18);
    border-color: rgba(108, 99, 255, 0.45);
    color: #fff;
    transform: translateY(-3px);
}

/* ── Navigation ── */
.footer-nav {
    flex: 0.8;
    min-width: 150px;
}
.footer-section-label {
    font-size: 11px;
    font-weight: 600;
    color: rgba(255, 255, 255, 0.35);
    text-transform: uppercase;
    letter-spacing: 1.2px;
    margin-bottom: 18px;
}
.footer-links {
    list-style: none;
    padding: 0;
    margin: 0;
    display: flex;
    flex-direction: column;
    gap: 10px;
}
.footer-link {
    font-size: 14px;
    color: rgba(255, 255, 255, 0.6);
    text-decoration: none;
    display: flex;
    align-items: center;
    gap: 8px;
    transition: color 0.2s ease, gap 0.2s ease;
}
.link-arrow {
    font-size: 12px;
    color: rgba(108, 99, 255, 0.5);
    transition: color 0.2s ease, transform 0.2s ease;
}
.footer-link:hover {
    color: #fff;
    gap: 12px;
}
.footer-link:hover .link-arrow {
    color: #6c63ff;
    transform: translateX(2px);
}

/* ── CTA ── */
.footer-cta {
    flex: 1;
    min-width: 200px;
}
.footer-cta-text {
    font-size: 14px;
    color: rgba(255, 255, 255, 0.55);
    line-height: 1.6;
    margin-bottom: 20px;
}
.footer-cta-btn {
    width: 100%;
    justify-content: center;
    margin-bottom: 16px;
    border-radius: 12px;
}
.footer-available {
    display: flex;
    align-items: center;
    gap: 8px;
    font-size: 12.5px;
    color: rgba(52, 211, 153, 0.85);
}
.available-dot {
    width: 7px;
    height: 7px;
    border-radius: 50%;
    background: #34d399;
    flex-shrink: 0;
    box-shadow: 0 0 8px rgba(52, 211, 153, 0.9);
    animation: footer-pulse 2s ease-in-out infinite;
}
@keyframes footer-pulse {
    0%, 100% { box-shadow: 0 0 6px rgba(52, 211, 153, 0.8); }
    50%       { box-shadow: 0 0 14px rgba(52, 211, 153, 1), 0 0 22px rgba(52, 211, 153, 0.4); }
}

/* ── Bottom Bar ── */
.footer-bottom {
    border-top: 1px solid rgba(255, 255, 255, 0.05);
    padding: 16px 0;
}
.footer-bottom-inner {
    display: flex;
    align-items: center;
    justify-content: space-between;
    flex-wrap: wrap;
    gap: 8px;
}
.footer-copy,
.footer-made {
    font-size: 12.5px;
    color: rgba(255, 255, 255, 0.3);
    margin: 0;
}

.back-to-top-btn {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    padding: 7px 18px;
    border-radius: 50px;
    background: rgba(108, 99, 255, 0.08);
    border: 1px solid rgba(108, 99, 255, 0.25);
    color: rgba(255, 255, 255, 0.85);
    font-size: 12.5px;
    font-weight: 500;
    text-decoration: none;
    transition: all 0.3s ease;
}
.back-to-top-btn svg {
    width: 14px;
    height: 14px;
    transition: transform 0.3s ease;
}
.back-to-top-btn:hover {
    background: linear-gradient(90deg, #6c63ff 0%, #9b59f5 100%);
    color: #ffffff;
    border-color: transparent;
    box-shadow: 0 4px 15px rgba(108, 99, 255, 0.4);
}
.back-to-top-btn:hover svg {
    transform: translateY(-2px);
}

/* ── Responsive ── */
@media screen and (max-width: 768px) {
    .footer-inner {
        flex-direction: column;
        gap: 36px;
        padding-top: 44px;
        padding-bottom: 36px;
    }
    .footer-brand { min-width: unset; }
    .footer-cta-btn { max-width: 280px; }
    .footer-bottom-inner { justify-content: center; text-align: center; }
}
</style>
