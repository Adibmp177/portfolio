<script setup>
import { ref, onMounted } from 'vue';

onMounted(() => {
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

    const wrapper = document.querySelector('.contactSection---wrapper');
    if (wrapper) Observer.observe(wrapper);
});

// ── Form State & Validation ───────────────────────────────
const getUserName = ref('');
const getUserEmail = ref('');
const getUserSubject = ref('');
const getUsersMessage = ref('');

const isNameValidat = ref(false);
const isEmailValidat = ref(false);
const isMessageValidat = ref(false);

const regEx_name = /^[a-zA-Z\s]+$/;
const regEx_email = /^[a-zA-Z0-9.!#$%&'*+/=?^_`{|}~-]+@[a-zA-Z0-9](?:[a-zA-Z0-9-]{0,61}[a-zA-Z0-9])?(?:\.[a-zA-Z0-9](?:[a-zA-Z0-9-]{0,61}[a-zA-Z0-9])?)*$/;

function addErrorClass(input) {
    if (input.nextElementSibling) input.nextElementSibling.classList.remove('yesError');
    input.classList.remove('invalid');
    input.classList.add('valid');
}
function removeErrorCalss(input) {
    if (input.nextElementSibling) input.nextElementSibling.classList.add('yesError');
    input.classList.remove('valid');
    input.classList.add('invalid');
}

function validateName(input) {
    const inputLength = input.value.trim().length >= 3;
    if (regEx_name.test(getUserName.value.trim()) && inputLength) {
        isNameValidat.value = true;
        addErrorClass(input);
    } else {
        isNameValidat.value = false;
        removeErrorCalss(input);
    }
}
function validateEmail(input) {
    if (regEx_email.test(getUserEmail.value.trim())) {
        isEmailValidat.value = true;
        addErrorClass(input);
    } else {
        isEmailValidat.value = false;
        removeErrorCalss(input);
    }
}
function validateMessage(input) {
    if (input.value.trim().length >= 15) {
        isMessageValidat.value = true;
        addErrorClass(input);
    } else {
        isMessageValidat.value = false;
        removeErrorCalss(input);
    }
}

function resetForm() {
    getUserName.value = '';
    getUserEmail.value = '';
    getUserSubject.value = '';
    getUsersMessage.value = '';
    isEmailValidat.value = false;
    isNameValidat.value = false;
    isMessageValidat.value = false;
    document.querySelectorAll('.input-field input, .input-field textarea').forEach((x) => x.classList.remove('valid', 'invalid'));
    document.querySelectorAll('.inputError').forEach((x) => x.classList.remove('yesError'));
}

// ── Copy to Clipboard Helper ──────────────────────────────
const copiedField = ref('');
function copyToClipboard(text, field) {
    if (navigator && navigator.clipboard) {
        navigator.clipboard.writeText(text);
        copiedField.value = field;
        setTimeout(() => {
            if (copiedField.value === field) copiedField.value = '';
        }, 2200);
    }
}

// ── Submission State ──────────────────────────────────────
const formLoading = ref(false);
const isSuccessful = ref(false);
const isError = ref(false);

async function sendEmail(e) {
    e.preventDefault();
    if (isNameValidat.value && isEmailValidat.value && isMessageValidat.value) {
        formLoading.value = true;
        let data = new FormData(e.target);

        fetch(e.target.action, {
            method: e.target.method,
            body: data,
            headers: { 'Accept': 'application/json' }
        }).then(response => {
            if (response.ok) {
                formLoading.value = false;
                isSuccessful.value = true;
                e.target.reset();
                resetForm();
            } else {
                formLoading.value = false;
                alert('Please try again later.');
            }
        }).catch(() => {
            alert('Network error. Please try again.');
            formLoading.value = false;
        });
    } else {
        isError.value = true;
        setTimeout(() => { isError.value = false; }, 3000);
    }
}
</script>

<template>
    <div class="contactSection---wrapper">
        <!-- Ambient Glow Orbs -->
        <div class="contact-glow-orb contact-glow-1"></div>
        <div class="contact-glow-orb contact-glow-2"></div>

        <div class="container">
            
            <!-- Section Heading -->
            <div class="heading--wrapper">
                <h2 class="heading">Contact me</h2>
            </div>

            <div class="contact-layout">
                
                <!-- ═══════════════════════════════════════════
                     LEFT SIDE: Narrative & Contact Info Cards
                ═══════════════════════════════════════════ -->
                <div class="contact-left">
                    <div class="contact-badge-top">
                        <span class="pulse-beacon"></span>
                        <span>Available for high-impact projects</span>
                    </div>

                    <h2 class="contact-title">
                        <span class="title-top">Have a bold product idea?</span>
                        <span class="title-gradient">Let's craft it together.</span>
                    </h2>
                    
                    <p class="contact-desc">
                        I specialize in turning intricate design challenges into clean, delightful digital experiences. Whether starting a new project or refining an existing product, let's build something exceptional.
                    </p>

                    <!-- Interactive Contact Info Cards with Color Glow on Hover -->
                    <div class="info-list">
                        <!-- Email Card -->
                        <div 
                            class="info-card info-card--email"
                            @click="copyToClipboard('Mohammadpouriadib@gmail.com', 'email')"
                            title="Click to copy email address"
                        >
                            <div class="info-icon email-bg">
                                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.8" stroke="currentColor">
                                    <path stroke-linecap="round" stroke-linejoin="round" d="M21.75 6.75v10.5a2.25 2.25 0 0 1-2.25 2.25h-15a2.25 2.25 0 0 1-2.25-2.25V6.75m19.5 0A2.25 2.25 0 0 0 19.5 4.5h-15a2.25 2.25 0 0 0-2.25 2.25m19.5 0v.243a2.25 2.25 0 0 1-1.07 1.916l-7.5 4.615a2.25 2.25 0 0 1-2.36 0L3.32 8.91a2.25 2.25 0 0 1-1.07-1.916V6.75" />
                                </svg>
                            </div>
                            <div class="info-text">
                                <span class="info-label">Direct Email</span>
                                <strong class="info-val">Mohammadpouriadib@gmail.com</strong>
                            </div>
                            <div class="copy-action-pill">
                                <span v-if="copiedField === 'email'" class="copied-indicator">✓ Copied!</span>
                                <span v-else class="copy-hint">Copy</span>
                            </div>
                        </div>

                        <!-- Phone Card -->
                        <div 
                            class="info-card info-card--phone"
                            @click="copyToClipboard('+989399866466', 'phone')"
                            title="Click to copy phone number"
                        >
                            <div class="info-icon phone-bg">
                                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.8" stroke="currentColor">
                                    <path stroke-linecap="round" stroke-linejoin="round" d="M2.25 6.75c0 8.284 6.716 15 15 15h2.25a2.25 2.25 0 0 0 2.25-2.25v-1.372c0-.516-.351-.966-.852-1.091l-4.423-1.106c-.44-.11-.902.055-1.173.417l-.97 1.293c-.282.376-.769.542-1.21.38a12.035 12.035 0 0 1-7.143-7.143c-.162-.441.004-.928.38-1.21l1.293-.97c.363-.271.527-.734.417-1.173L6.963 3.102a1.125 1.125 0 0 0-1.091-.852H4.5A2.25 2.25 0 0 0 2.25 4.5v2.25Z" />
                                </svg>
                            </div>
                            <div class="info-text">
                                <span class="info-label">Direct Phone & WhatsApp</span>
                                <strong class="info-val">+98 939 986 6466</strong>
                            </div>
                            <div class="copy-action-pill">
                                <span v-if="copiedField === 'phone'" class="copied-indicator">✓ Copied!</span>
                                <span v-else class="copy-hint">Copy</span>
                            </div>
                        </div>

                        <!-- Location & Timezone Card -->
                        <div class="info-card info-card--location">
                            <div class="info-icon loc-bg">
                                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.8" stroke="currentColor">
                                    <path stroke-linecap="round" stroke-linejoin="round" d="M15 10.5a3 3 0 1 1-6 0 3 3 0 0 1 6 0Z" />
                                    <path stroke-linecap="round" stroke-linejoin="round" d="M19.5 10.5c0 7.142-7.5 11.25-7.5 11.25S4.5 17.642 4.5 10.5a7.5 7.5 0 1 1 15 0Z" />
                                </svg>
                            </div>
                            <div class="info-text">
                                <span class="info-label">Location & Timezone</span>
                                <strong class="info-val">Sardasht, Iran <span class="tz-pill">UTC+3:30</span></strong>
                            </div>
                        </div>
                    </div>

                    <!-- Trust & Response Guarantee Banner -->
                    <div class="trust-guarantee-box">
                        <div class="trust-item">
                            <span class="trust-icon">⚡</span>
                            <span>Response within <strong>24 Hours</strong></span>
                        </div>
                        <div class="trust-item">
                            <span class="trust-icon">🔒</span>
                            <span><strong>NDA & Confidentiality</strong> Protected</span>
                        </div>
                    </div>
                </div>

                <!-- ═══════════════════════════════════════════
                     RIGHT SIDE: Clean Design Message Form
                ═══════════════════════════════════════════ -->
                <div class="contact-right">
                    <div class="form-card-modern">
                        <div class="form-header-bar">
                            <div class="form-header-title">Send a Message</div>
                            <span class="form-dot-active"></span>
                        </div>

                        <form class="form" action="https://formspree.io/f/xgegyvjp" method="post" @submit="sendEmail($event)">
                            
                            <!-- Row 1: Name & Email -->
                            <div class="form-row">
                                <div class="input-field">
                                    <label for="name">Your Name</label>
                                    <input 
                                        type="text" 
                                        name="name" 
                                        id="name" 
                                        class="input" 
                                        placeholder="e.g. Alex Morgan" 
                                        autocomplete="off" 
                                        v-model="getUserName" 
                                        @focusout="validateName($event.currentTarget)"
                                    >
                                    <div class="inputError">
                                        <div class="errorTxt"><div class="circle"></div>At least 3 letters required</div>
                                    </div>
                                </div>

                                <div class="input-field">
                                    <label for="email">Email Address</label>
                                    <input 
                                        type="email" 
                                        name="email" 
                                        id="email" 
                                        class="input" 
                                        placeholder="alex@company.com" 
                                        autocomplete="off" 
                                        v-model="getUserEmail" 
                                        @focusout="validateEmail($event.currentTarget)"
                                    >
                                    <div class="inputError">
                                        <div class="errorTxt"><div class="circle"></div>Enter a valid email address</div>
                                    </div>
                                </div>
                            </div>

                            <!-- Row 2: Subject (Optional) -->
                            <div class="input-field">
                                <label for="subject">Subject <span class="optional-txt">(optional)</span></label>
                                <input 
                                    type="text" 
                                    name="subject" 
                                    id="subject" 
                                    class="input" 
                                    placeholder="Project scope or inquiry title" 
                                    autocomplete="off" 
                                    v-model="getUserSubject"
                                >
                            </div>

                            <!-- Row 3: Message -->
                            <div class="input-field">
                                <div class="textarea-header">
                                    <label for="txt">Message</label>
                                    <span class="char-count" :class="{ 'char-count--valid': getUsersMessage.length >= 15 }">
                                        {{ getUsersMessage.length }}/15+ chars
                                    </span>
                                </div>
                                <textarea 
                                    name="message" 
                                    id="txt" 
                                    rows="5" 
                                    placeholder="Describe your project goals, timeline, or requirements..." 
                                    autocomplete="off" 
                                    v-model="getUsersMessage" 
                                    @focusout="validateMessage($event.currentTarget)"
                                ></textarea>
                                <div class="inputError">
                                    <div class="errorTxt"><div class="circle"></div>Please share at least 15 characters</div>
                                </div>
                            </div>

                            <!-- Submit Button -->
                            <button type="submit" class="cta-btn cta-btn--primary form-submit-btn" :disabled="formLoading">
                                <span v-if="formLoading" class="loader-spinner"></span>
                                <template v-else>
                                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor" class="btn-icon">
                                        <path stroke-linecap="round" stroke-linejoin="round" d="M6 12 3.269 3.125A59.769 59.769 0 0 1 21.485 12 59.768 59.768 0 0 1 3.27 20.875L5.999 12Zm0 0h7.5" />
                                    </svg>
                                    <span class="btn-label">Send Message</span>
                                </template>
                            </button>

                        </form>

                        <!-- Error Toast -->
                        <Transition name="fade">
                            <div class="formPopUp formPopUp--error" v-if="isError">
                                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.8" stroke="currentColor" class="popIcon">
                                    <path stroke-linecap="round" stroke-linejoin="round" d="m9.75 9.75 4.5 4.5m0-4.5-4.5 4.5M21 12a9 9 0 1 1-18 0 9 9 0 0 1 18 0Z" />
                                </svg>
                                <p class="popUoTxt">Please fill out all required fields with valid information.</p>
                            </div>
                        </Transition>
                    </div>
                </div>

            </div>

        </div>

        <!-- ── Professional Success Popup Modal ── -->
        <Teleport to="body">
            <Transition name="modal">
                <div class="modal-overlay" v-if="isSuccessful" @click="isSuccessful = false">
                    <div class="modal-card" @click.stop>
                        <div class="modal-icon-glow">
                            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="2.5" stroke="currentColor">
                                <path stroke-linecap="round" stroke-linejoin="round" d="m4.5 12.75 6 6 9-13.5" />
                            </svg>
                        </div>
                        <h3 class="modal-title">Message Sent Successfully!</h3>
                        <p class="modal-desc">
                            پیام شما با موفقیت ارسال شد و در اسرع وقت پاسخ داده خواهد شد.<br>
                            <span class="modal-desc-en">Thank you for reaching out! I will review your project details and get back to you within 24 hours.</span>
                        </p>
                        <button class="cta-btn cta-btn--primary modal-close-btn" @click="isSuccessful = false">
                            <span>Done</span>
                        </button>
                    </div>
                </div>
            </Transition>
        </Teleport>

    </div>
</template>

<style scoped>
/* ── Wrapper & Ambient Atmosphere ── */
.contactSection---wrapper {
    position: relative;
    padding: 100px 0;
    overflow: hidden;
    width: 100%;
    max-width: 100%;
    box-sizing: border-box;
}

/* Ambient glow orbs */
.contact-glow-orb {
    position: absolute;
    border-radius: 50%;
    filter: blur(120px);
    pointer-events: none;
    z-index: 0;
    opacity: 0.16;
}
.contact-glow-1 {
    width: 480px;
    height: 480px;
    background: radial-gradient(circle, #6c63ff 0%, rgba(108, 99, 255, 0) 70%);
    top: 20%;
    left: -140px;
}
.contact-glow-2 {
    width: 440px;
    height: 440px;
    background: radial-gradient(circle, #9b59f5 0%, rgba(155, 89, 245, 0) 70%);
    bottom: 15%;
    right: -100px;
}

.container {
    position: relative;
    z-index: 1;
}

/* Heading animation */
.contactSection---wrapper .heading--wrapper {
    opacity: 0;
    transform: translateY(-24px);
    transition: opacity 0.8s cubic-bezier(0.22, 1, 0.36, 1), transform 0.8s cubic-bezier(0.22, 1, 0.36, 1);
    margin-bottom: 48px;
}
.active--s .heading--wrapper {
    opacity: 1;
    transform: translateY(0);
}

/* ── Main Layout ── */
.contact-layout {
    display: grid;
    grid-template-columns: minmax(0, 1fr) minmax(0, 1.15fr);
    gap: clamp(24px, 3.5vw, 48px);
    align-items: stretch;
    width: 100%;
    max-width: 100%;
    box-sizing: border-box;
}

/* ── Left Column ── */
.contact-left {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    gap: 18px;
    opacity: 0;
    transform: translateX(-40px);
    transition: opacity 0.85s 0.15s cubic-bezier(0.22, 1, 0.36, 1), transform 0.85s 0.15s cubic-bezier(0.22, 1, 0.36, 1);
    min-width: 0;
    width: 100%;
    max-width: 100%;
    box-sizing: border-box;
}
.active--s .contact-left {
    opacity: 1;
    transform: translateX(0);
}

.contact-badge-top {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    padding: 4px 12px;
    border-radius: 20px;
    background: rgba(52, 211, 153, 0.1);
    border: 1px solid rgba(52, 211, 153, 0.3);
    font-size: 11.5px;
    color: #34d399;
    font-weight: 500;
    width: fit-content;
}
.pulse-beacon {
    width: 6px;
    height: 6px;
    border-radius: 50%;
    background: #34d399;
    box-shadow: 0 0 8px #34d399;
    animation: beaconPulse 2s infinite;
}
@keyframes beaconPulse {
    0%, 100% { opacity: 1; transform: scale(1); }
    50% { opacity: 0.5; transform: scale(1.3); }
}

.contact-title {
    display: flex;
    flex-direction: column;
    line-height: 1.22;
    margin: 0;
}
.title-top {
    font-size: 22px;
    font-weight: 400;
    color: rgba(255, 255, 255, 0.8);
    margin-bottom: 4px;
}
.title-gradient {
    font-family: var(--font-display);
    font-size: clamp(26px, 3.2vw, 36px);
    font-weight: 600;
    letter-spacing: 0.4px;
    background: linear-gradient(135deg, #ffffff 20%, #a78bfa 60%, #6c63ff 100%);
    -webkit-background-clip: text;
    background-clip: text;
    color: transparent;
}

.contact-desc {
    font-size: 14.5px;
    color: rgba(255, 255, 255, 0.68);
    line-height: 1.7;
    margin: 0;
}

/* ── Interactive Info List with Custom Color Hover Shadows ── */
.info-list {
    display: flex;
    flex-direction: column;
    gap: 14px;
    margin-top: 4px;
    width: 100%;
    max-width: 100%;
    box-sizing: border-box;
}

.info-card {
    display: flex;
    align-items: center;
    gap: 16px;
    background: rgba(16, 14, 38, 0.8);
    border: 1px solid rgba(255, 255, 255, 0.08);
    border-radius: 20px;
    padding: 14px 18px;
    backdrop-filter: blur(12px);
    -webkit-backdrop-filter: blur(12px);
    box-shadow: inset 0 1px 1px rgba(255, 255, 255, 0.08), 0 10px 30px rgba(0, 0, 0, 0.35);
    transition: all 0.3s cubic-bezier(0.22, 1, 0.36, 1);
    position: relative;
    cursor: pointer;
    min-width: 0;
    width: 100%;
    max-width: 100%;
    box-sizing: border-box;
}

/* 1. Email: Purple/Indigo Hover Glow */
.info-card--email:hover {
    background: rgba(108, 99, 255, 0.08);
    border-color: rgba(108, 99, 255, 0.45);
    transform: translateY(-3px);
    box-shadow: inset 0 1px 1px rgba(255, 255, 255, 0.12), 0 12px 30px rgba(0, 0, 0, 0.45), 0 0 22px rgba(108, 99, 255, 0.3);
}

/* 2. Phone: Emerald/Green Hover Glow */
.info-card--phone:hover {
    background: rgba(16, 185, 129, 0.08);
    border-color: rgba(16, 185, 129, 0.45);
    transform: translateY(-3px);
    box-shadow: inset 0 1px 1px rgba(255, 255, 255, 0.12), 0 12px 30px rgba(0, 0, 0, 0.45), 0 0 22px rgba(16, 185, 129, 0.3);
}

/* 3. Location: Amber/Yellow Hover Glow */
.info-card--location:hover {
    background: rgba(245, 158, 11, 0.08);
    border-color: rgba(245, 158, 11, 0.45);
    transform: translateY(-3px);
    box-shadow: inset 0 1px 1px rgba(255, 255, 255, 0.12), 0 12px 30px rgba(0, 0, 0, 0.45), 0 0 22px rgba(245, 158, 11, 0.3);
}

.info-icon {
    width: 42px;
    height: 42px;
    border-radius: 12px;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-shrink: 0;
    transition: transform 0.3s ease;
}
.info-card:hover .info-icon {
    transform: scale(1.08);
}
.info-icon svg { width: 20px; height: 20px; }

.email-bg { color: #818cf8; background: rgba(108, 99, 255, 0.15); }
.phone-bg { color: #34d399; background: rgba(16, 185, 129, 0.15); }
.loc-bg   { color: #fbbf24; background: rgba(245, 158, 11, 0.15); }

.info-text {
    display: flex;
    flex-direction: column;
    flex: 1;
    min-width: 0;
    overflow: hidden;
}
.info-label {
    font-size: 11px;
    color: rgba(255, 255, 255, 0.45);
    text-transform: uppercase;
    letter-spacing: 0.8px;
    margin-bottom: 2px;
}
.info-val {
    font-size: 14px;
    color: #ffffff;
    font-weight: 500;
    word-break: break-word;
    overflow-wrap: anywhere;
}

.tz-pill {
    font-size: 11px;
    color: #fbbf24;
    background: rgba(245, 158, 11, 0.15);
    padding: 1px 6px;
    border-radius: 4px;
    margin-left: 6px;
    font-weight: 400;
}

.copy-action-pill {
    font-size: 11px;
    font-weight: 600;
    padding: 4px 10px;
    border-radius: 20px;
    background: rgba(255, 255, 255, 0.05);
    border: 1px solid rgba(255, 255, 255, 0.1);
    color: rgba(255, 255, 255, 0.7);
    transition: all 0.2s ease;
    flex-shrink: 0;
    white-space: nowrap;
}
.info-card--email:hover .copy-action-pill {
    background: rgba(108, 99, 255, 0.2);
    border-color: rgba(155, 89, 245, 0.5);
    color: #fff;
}
.info-card--phone:hover .copy-action-pill {
    background: rgba(16, 185, 129, 0.2);
    border-color: rgba(52, 211, 153, 0.5);
    color: #fff;
}
.copied-indicator {
    color: #34d399 !important;
}

/* Trust Box */
.trust-guarantee-box {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 12px;
    background: rgba(255, 255, 255, 0.02);
    border: 1px solid rgba(255, 255, 255, 0.06);
    border-radius: 14px;
    padding: 12px 16px;
    margin-top: 4px;
    width: 100%;
    max-width: 100%;
    box-sizing: border-box;
}
.trust-item {
    display: flex;
    align-items: center;
    gap: 8px;
    font-size: 12px;
    color: rgba(255, 255, 255, 0.65);
}
.trust-item strong {
    color: rgba(255, 255, 255, 0.95);
}
.trust-icon { font-size: 13px; }

/* ── Right Column: Form Card ── */
.contact-right {
    opacity: 0;
    transform: translateX(40px);
    transition: opacity 0.85s 0.25s cubic-bezier(0.22, 1, 0.36, 1), transform 0.85s 0.25s cubic-bezier(0.22, 1, 0.36, 1);
    min-width: 0;
    width: 100%;
    max-width: 100%;
    box-sizing: border-box;
}
.active--s .contact-right {
    opacity: 1;
    transform: translateX(0);
}

.form-card-modern {
    background: rgba(16, 14, 38, 0.85);
    border: 1px solid rgba(255, 255, 255, 0.1);
    border-radius: 22px;
    padding: 32px 30px;
    backdrop-filter: blur(18px);
    -webkit-backdrop-filter: blur(18px);
    box-shadow: inset 0 1px 1px rgba(255, 255, 255, 0.1), 0 20px 50px rgba(0, 0, 0, 0.5), 0 0 30px rgba(108, 99, 255, 0.08);
    position: relative;
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    min-width: 0;
    width: 100%;
    max-width: 100%;
    box-sizing: border-box;
}

.form-header-bar {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 20px;
    padding-bottom: 14px;
    border-bottom: 1px solid rgba(255, 255, 255, 0.06);
}
.form-header-title {
    font-family: var(--font-display);
    font-size: 16px;
    font-weight: 600;
    letter-spacing: 0.3px;
    color: #ffffff;
}
.form-dot-active {
    width: 6px;
    height: 6px;
    border-radius: 50%;
    background: #6c63ff;
    box-shadow: 0 0 8px #6c63ff;
}

.form {
    display: flex;
    flex-direction: column;
    gap: 18px;
    flex: 1;
    justify-content: space-between;
    width: 100%;
    max-width: 100%;
    box-sizing: border-box;
}

/* ── Inputs ── */
.form-row {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 16px;
    width: 100%;
    max-width: 100%;
    box-sizing: border-box;
}

.input-field {
    display: flex;
    flex-direction: column;
    position: relative;
    width: 100%;
    max-width: 100%;
    box-sizing: border-box;
    min-width: 0;
}

.input-field label {
    font-size: 12.5px;
    color: rgba(255, 255, 255, 0.75);
    margin-bottom: 6px;
    font-weight: 500;
}
.optional-txt {
    font-size: 11px;
    color: rgba(255, 255, 255, 0.4);
    font-weight: 400;
}

.textarea-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 6px;
}
.textarea-header label { margin-bottom: 0; }
.char-count {
    font-size: 11px;
    color: rgba(255, 255, 255, 0.4);
    font-family: monospace;
}
.char-count--valid {
    color: #34d399;
}

.input-field input,
.input-field textarea {
    width: 100%;
    background: rgba(255, 255, 255, 0.025);
    border: 1px solid rgba(255, 255, 255, 0.09);
    border-radius: 12px;
    padding: 12px 14px;
    color: #ffffff;
    font-family: var(--font-body);
    font-size: 13.5px;
    outline: none;
    transition: all 0.25s ease;
}
.input-field input::placeholder,
.input-field textarea::placeholder {
    color: rgba(255, 255, 255, 0.3);
}
.input-field input:focus,
.input-field textarea:focus {
    border-color: rgba(155, 89, 245, 0.6);
    background: rgba(108, 99, 255, 0.06);
    box-shadow: 0 0 0 3px rgba(108, 99, 255, 0.2), 0 0 15px rgba(108, 99, 255, 0.12);
}

.inputError {
    display: none;
    font-size: 11.5px;
    color: #f87171;
    margin-top: 4px;
}
.inputError.yesError {
    display: block;
}
.circle {
    width: 5px;
    height: 5px;
    border-radius: 50%;
    background: #f87171;
    display: inline-block;
    margin-right: 5px;
}

/* ── Submit Button ── */
.form-submit-btn {
    width: 100%;
    padding: 14px;
    font-size: 14.5px;
    margin-top: 4px;
    border-radius: 12px;
    display: inline-flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
    color: #fff;
    background: linear-gradient(135deg, #6c63ff 0%, #9b59f5 50%, #6c63ff 100%);
    background-size: 200% 100%;
    border: none;
    cursor: pointer;
    box-shadow: 0 6px 22px rgba(108, 99, 255, 0.45);
    transition: all 0.3s ease;
}
.form-submit-btn:hover:not(:disabled) {
    background-position: right center;
    box-shadow: 0 10px 30px rgba(155, 89, 245, 0.6);
    transform: translateY(-2px);
}
.form-submit-btn:disabled {
    opacity: 0.7;
    cursor: not-allowed;
}
.btn-icon { width: 17px; height: 17px; }

.loader-spinner {
    width: 18px;
    height: 18px;
    border: 2px solid rgba(255, 255, 255, 0.3);
    border-radius: 50%;
    border-top-color: #fff;
    animation: spin 0.8s linear infinite;
}
@keyframes spin {
    to { transform: rotate(360deg); }
}

/* ── Toast Popups ── */
.formPopUp {
    display: flex;
    align-items: center;
    gap: 10px;
    padding: 11px 16px;
    border-radius: 12px;
    margin-top: 12px;
    font-size: 13px;
}
.formPopUp--error {
    background: rgba(239, 68, 68, 0.15);
    border: 1px solid rgba(239, 68, 68, 0.4);
    color: #fca5a5;
}
.popIcon { width: 18px; height: 18px; flex-shrink: 0; }
.popUoTxt { margin: 0; }

/* ── Success Modal ── */
.modal-overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    background: rgba(8, 7, 20, 0.8);
    backdrop-filter: blur(12px);
    -webkit-backdrop-filter: blur(12px);
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 99999;
    padding: 20px;
}
.modal-card {
    background: #12102e;
    border: 1px solid rgba(155, 89, 245, 0.4);
    border-radius: 24px;
    padding: 38px 32px;
    max-width: 460px;
    width: 100%;
    text-align: center;
    box-shadow: 0 25px 60px rgba(0, 0, 0, 0.6), 0 0 40px rgba(108, 99, 255, 0.25);
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 16px;
}
.modal-icon-glow {
    width: 60px;
    height: 60px;
    border-radius: 50%;
    background: rgba(52, 211, 153, 0.15);
    color: #34d399;
    border: 1px solid rgba(52, 211, 153, 0.4);
    display: flex;
    align-items: center;
    justify-content: center;
    box-shadow: 0 0 25px rgba(52, 211, 153, 0.3);
}
.modal-icon-glow svg { width: 28px; height: 28px; }

.modal-title {
    font-family: var(--font-display);
    font-size: 21px;
    font-weight: 600;
    color: #ffffff;
    margin: 0;
}
.modal-desc {
    font-size: 14px;
    color: rgba(255, 255, 255, 0.85);
    line-height: 1.6;
    margin: 0;
    direction: rtl;
}
.modal-desc-en {
    display: block;
    direction: ltr;
    margin-top: 6px;
    font-size: 13px;
    color: rgba(255, 255, 255, 0.6);
}
.modal-close-btn {
    margin-top: 4px;
    width: 130px;
    padding: 10px 0;
    border-radius: 50px;
    font-size: 13.5px;
}

/* Modal Transition */
.modal-enter-active, .modal-leave-active {
    transition: opacity 0.3s ease, transform 0.3s cubic-bezier(0.34, 1.56, 0.64, 1);
}
.modal-enter-from, .modal-leave-to {
    opacity: 0;
    transform: scale(0.9);
}

/* ── Responsive Queries ── */
@media screen and (max-width: 991px) {
    .contact-layout {
        grid-template-columns: minmax(0, 1fr);
        gap: 36px;
    }
    .trust-guarantee-box {
        flex-direction: column;
        align-items: flex-start;
        gap: 8px;
    }
    .form-card-modern {
        height: auto;
    }
}

@media screen and (max-width: 768px) {
    .contactSection---wrapper {
        padding: 64px 0;
    }
    .contactSection---wrapper .heading--wrapper {
        margin-bottom: 36px;
    }
    .contact-left {
        transform: translateY(24px);
    }
    .contact-right {
        transform: translateY(24px);
    }
    .active--s .contact-left,
    .active--s .contact-right {
        transform: translateY(0);
    }
    .form-card-modern {
        padding: 24px 20px;
        border-radius: 20px;
    }
    .form-row {
        grid-template-columns: 1fr;
        gap: 14px;
    }
}

@media screen and (max-width: 480px) {
    .info-card {
        padding: 12px 14px;
        gap: 12px;
        border-radius: 16px;
    }
    .info-icon {
        width: 38px;
        height: 38px;
        border-radius: 10px;
    }
    .info-icon svg {
        width: 18px;
        height: 18px;
    }
    .info-val {
        font-size: 12.5px;
    }
    .copy-action-pill {
        padding: 3px 8px;
        font-size: 10.5px;
    }
    .form-card-modern {
        padding: 20px 16px;
        border-radius: 18px;
    }
    .trust-guarantee-box {
        padding: 10px 14px;
    }
}
</style>