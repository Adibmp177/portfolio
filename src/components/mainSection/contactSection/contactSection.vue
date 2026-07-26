<script setup>
import { ref } from 'vue';

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
function resetForm() {
    getUserName.value = '';
    getUserEmail.value = '';
    getUserSubject.value = '';
    getUsersMessage.value = '';
    isEmailValidat.value = false;
    isNameValidat.value = false;
    isMessageValidat.value = false;
    document.querySelectorAll('.input').forEach((x) => x.classList.remove('valid', 'invalid'));
    document.querySelectorAll('.inputError').forEach((x) => x.classList.remove('yesError'));
}

const getUserName = ref('');
const getUserEmail = ref('');
const getUserSubject = ref('');
const getUsersMessage = ref('');

const isNameValidat = ref(false);
const isEmailValidat = ref(false);
const isMessageValidat = ref(false);

const regEx_name = /^[a-zA-Z\s]+$/;
const regEx_email = /^[a-zA-Z0-9.!#$%&'*+/=?^_`{|}~-]+@[a-zA-Z0-9](?:[a-zA-Z0-9-]{0,61}[a-zA-Z0-9])?(?:\.[a-zA-Z0-9](?:[a-zA-Z0-9-]{0,61}[a-zA-Z0-9])?)*$/;

function validateName(input) {
    const inputLength = input.value.length >= 3;
    if (regEx_name.test(getUserName.value) && inputLength) {
        isNameValidat.value = true;
        addErrorClass(input);
    } else {
        isNameValidat.value = false;
        removeErrorCalss(input);
    }
}
function validateEmail(input) {
    if (regEx_email.test(getUserEmail.value)) {
        isEmailValidat.value = true;
        addErrorClass(input);
    } else {
        isEmailValidat.value = false;
        removeErrorCalss(input);
    }
}
function validateMessage(input) {
    if (input.value.length >= 15) {
        isMessageValidat.value = true;
        addErrorClass(input);
    } else {
        isMessageValidat.value = false;
        removeErrorCalss(input);
    }
}

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
                setTimeout(() => { isSuccessful.value = false; }, 2500);
                e.target.reset();
                resetForm();
            } else {
                formLoading.value = false;
                alert('Please try again');
            }
        }).catch(() => {
            alert('Please try again');
            formLoading.value = false;
        });
    } else {
        isError.value = true;
        setTimeout(() => { isError.value = false; }, 2500);
    }
}
</script>

<template>
    <div class="contactSection---wrapper">
        <div class="container">
            
            <!-- Heading -->
            <div class="heading--wrapper">
                <h1 class="heading">Contact me</h1>
            </div>

            <div class="contact-layout">
                
                <!-- Left Side: Text, Info, Social Icons -->
                <div class="contact-left">
                    <h2 class="contact-title">
                        <span class="title-top">Have a brilliant idea?</span>
                        <span class="title-gradient">Let's Design it together.</span>
                    </h2>
                    
                    <p class="contact-desc">
                        I turn complex ideas into clean, beautiful, and easy-to-use apps and websites. Whether you are building a new product from scratch or fixing an old one, I am here to help. Let's bring your vision to life!
                    </p>

                    <!-- Contact Info Items -->
                    <div class="info-list">
                        <!-- Email -->
                        <div class="info-card">
                            <div class="info-icon email-bg">
                                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor">
                                    <path stroke-linecap="round" stroke-linejoin="round" d="M21.75 6.75v10.5a2.25 2.25 0 0 1-2.25 2.25h-15a2.25 2.25 0 0 1-2.25-2.25V6.75m19.5 0A2.25 2.25 0 0 0 19.5 4.5h-15a2.25 2.25 0 0 0-2.25 2.25m19.5 0v.243a2.25 2.25 0 0 1-1.07 1.916l-7.5 4.615a2.25 2.25 0 0 1-2.36 0L3.32 8.91a2.25 2.25 0 0 1-1.07-1.916V6.75" />
                                </svg>
                            </div>
                            <div class="info-text">
                                <span class="info-label">Email</span>
                                <strong class="info-val">Mohammadpouriadib@gmail.com</strong>
                            </div>
                        </div>

                        <!-- Phone -->
                        <div class="info-card">
                            <div class="info-icon phone-bg">
                                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor">
                                    <path stroke-linecap="round" stroke-linejoin="round" d="M2.25 6.75c0 8.284 6.716 15 15 15h2.25a2.25 2.25 0 0 0 2.25-2.25v-1.372c0-.516-.351-.966-.852-1.091l-4.423-1.106c-.44-.11-.902.055-1.173.417l-.97 1.293c-.282.376-.769.542-1.21.38a12.035 12.035 0 0 1-7.143-7.143c-.162-.441.004-.928.38-1.21l1.293-.97c.363-.271.527-.734.417-1.173L6.963 3.102a1.125 1.125 0 0 0-1.091-.852H4.5A2.25 2.25 0 0 0 2.25 4.5v2.25Z" />
                                </svg>
                            </div>
                            <div class="info-text">
                                <span class="info-label">Phone</span>
                                <strong class="info-val">+989399866466</strong>
                            </div>
                        </div>

                        <!-- Location -->
                        <div class="info-card">
                            <div class="info-icon loc-bg">
                                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor">
                                    <path stroke-linecap="round" stroke-linejoin="round" d="M15 10.5a3 3 0 1 1-6 0 3 3 0 0 1 6 0Z" />
                                    <path stroke-linecap="round" stroke-linejoin="round" d="M19.5 10.5c0 7.142-7.5 11.25-7.5 11.25S4.5 17.642 4.5 10.5a7.5 7.5 0 1 1 15 0Z" />
                                </svg>
                            </div>
                            <div class="info-text">
                                <span class="info-label">Location</span>
                                <strong class="info-val">IRAN, Sardasht</strong>
                            </div>
                        </div>
                    </div>

                    <!-- Connect with me & Social Icons -->
                    <div class="connect-wrapper">
                        <span class="connect-label">Connect with me</span>
                        <div class="social--wrapper">
                            <!-- Figma -->
                            <a href="https://www.figma.com/@adibmohammadpou" class="social-icon" aria-label="Figma" target="_blank" rel="noopener noreferrer">
                                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 38 57" fill="currentColor">
                                    <path d="M19 28.5a9.5 9.5 0 1 1 19 0 9.5 9.5 0 0 1-19 0Z"/>
                                    <path d="M0 47.5A9.5 9.5 0 0 1 9.5 38H19v9.5a9.5 9.5 0 0 1-19 0Z"/>
                                    <path d="M19 0v19h9.5a9.5 9.5 0 0 0 0-19H19Z"/>
                                    <path d="M0 9.5A9.5 9.5 0 0 0 9.5 19H19V0H9.5A9.5 9.5 0 0 0 0 9.5Z"/>
                                    <path d="M0 28.5A9.5 9.5 0 0 0 9.5 38H19V19H9.5A9.5 9.5 0 0 0 0 28.5Z"/>
                                </svg>
                            </a>
                            <!-- LinkedIn -->
                            <a href="https://www.linkedin.com/in/adibmohammadpouri/" class="social-icon" aria-label="LinkedIn" target="_blank" rel="noopener noreferrer">
                                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor">
                                    <path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433a2.062 2.062 0 0 1-2.063-2.065 2.064 2.064 0 1 1 2.063 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/>
                                </svg>
                            </a>
                            <!-- Telegram -->
                            <a href="https://t.me/Adibmohamadpori" class="social-icon" aria-label="Telegram" target="_blank" rel="noopener noreferrer">
                                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor">
                                    <path d="M12 0C5.373 0 0 5.373 0 12s5.373 12 12 12 12-5.373 12-12S18.627 0 12 0Zm5.562 8.248-2.04 9.617c-.152.672-.554.836-1.123.52l-3.1-2.285-1.495 1.438c-.165.165-.304.304-.624.304l.223-3.167 5.754-5.195c.25-.223-.054-.347-.388-.124L7.29 14.806l-3.045-.953c-.663-.207-.677-.663.138-.98l11.893-4.585c.551-.199 1.033.134.857.98l-.571-.02Z"/>
                                </svg>
                            </a>
                            <!-- Dribbble -->
                            <a href="https://dribbble.com/adibmohammadpouri" class="social-icon" aria-label="Dribbble" target="_blank" rel="noopener noreferrer">
                                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor">
                                    <path d="M12 2a10 10 0 1 0 10 10A10.011 10.011 0 0 0 12 2zm6.75 6.09a8.02 8.02 0 0 1 2.06 5.25c-.32-.05-3.83-.56-7.38-.07a41.87 41.87 0 0 0-.74-1.52c3.55-1.41 5.04-3.1 5.17-3.25a7.9 7.9 0 0 1 .89-.41zm-1.82-.77c-.12.14-1.49 1.7-4.85 3.01a45.69 45.69 0 0 0-3.3-4.94A8.07 8.07 0 0 1 12 4a7.94 7.94 0 0 1 4.93 1.32zM8.34 2.8a44.62 44.62 0 0 1 3.23 4.88c-3.79 1.05-7.14 1.04-7.5 1.04a7.99 7.99 0 0 1 4.27-5.92zm-5.18 7.4c.39 0 3.38.01 7.02-.97.26.51.51 1.03.75 1.55-3.84 1.09-7.34 1.57-7.69 1.62a8.04 8.04 0 0 1-.08-2.2zm1.2 3.81c.32-.04 3.49-.49 7.15-1.53.86 2.37 1.37 4.74 1.54 5.67A8.02 8.02 0 0 1 4.36 14.01zm9.4 6.8c-.18-.97-.66-3.28-1.5-5.59 3.3-.43 6.55.03 6.87.08a8.02 8.02 0 0 1-5.37 5.51z"/>
                                </svg>
                            </a>
                        </div>
                    </div>
                </div>

                <!-- Right Side: Form Card Container -->
                <div class="contact-right">
                    <div class="form-card">
                        <form class="form" action="https://formspree.io/f/xgegyvjp" method="post" @submit="sendEmail($event)">
                            
                            <!-- Row 1: Name & Email -->
                            <div class="form-row">
                                <div class="input-field">
                                    <label for="name">Name</label>
                                    <input type="text" name="name" id="name" class="input" placeholder="Enter your name here" autocomplete="off" v-model="getUserName" @focusout="validateName($event.currentTarget)">
                                    <div class="inputError">
                                        <div class="errorTxt errorTxt-1"><div class="circle"></div>Enter text only</div>
                                        <div class="errorTxt errorTxt-2"><div class="circle"></div>At least 3 characters</div>
                                    </div>
                                </div>

                                <div class="input-field">
                                    <label for="email">Email</label>
                                    <input type="email" name="email" id="email" class="input" placeholder="Your email address" autocomplete="off" v-model="getUserEmail" @focusout="validateEmail($event.currentTarget)">
                                    <div class="inputError">
                                        <div class="errorTxt errorTxt-1"><div class="circle"></div>Enter a valid email address</div>
                                    </div>
                                </div>
                            </div>

                            <!-- Row 2: Subject (Optional) -->
                            <div class="input-field">
                                <label for="subject">Subject <span class="optional-txt">(optional)</span></label>
                                <input type="text" name="subject" id="subject" class="input" placeholder="Enter the subject" autocomplete="off" v-model="getUserSubject">
                            </div>

                            <!-- Row 3: Message -->
                            <div class="input-field">
                                <label for="txt">Message</label>
                                <textarea name="message" id="txt" rows="5" placeholder="Enter your message" autocomplete="off" v-model="getUsersMessage" @focusout="validateMessage($event.currentTarget)"></textarea>
                                <div class="inputError">
                                    <div class="errorTxt errorTxt-1"><div class="circle"></div>Please enter at least 15 characters</div>
                                </div>
                            </div>

                            <!-- Submit Button -->
                            <button type="submit" class="cta-btn cta-btn--primary form-submit-btn">
                                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="btn-icon">
                                    <path stroke-linecap="round" stroke-linejoin="round" d="M6 12 3.269 3.125A59.769 59.769 0 0 1 21.485 12 59.768 59.768 0 0 1 3.27 20.875L5.999 12Zm0 0h7.5" />
                                </svg>
                                <span class="btn-label">Send Message</span>
                            </button>

                        </form>

                        <div class="formLoading" v-if="formLoading"><span class="loader"></span></div>

                        <Transition>
                            <div class="formPopUp formPopUp--error" v-if="isError">
                                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="popIcon">
                                    <path stroke-linecap="round" stroke-linejoin="round" d="m9.75 9.75 4.5 4.5m0-4.5-4.5 4.5M21 12a9 9 0 1 1-18 0 9 9 0 0 1 18 0Z" />
                                </svg>
                                <p class="popUoTxt">Please fill out all fields correctly.</p>
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
                            <span class="modal-desc-en">Thank you for reaching out! I will review your message and reply as soon as possible.</span>
                        </p>
                        <button class="cta-btn cta-btn--primary modal-close-btn" @click="isSuccessful = false">
                            <span>Close</span>
                        </button>
                    </div>
                </div>
            </Transition>
        </Teleport>

    </div>
</template>

<style scoped>
.contactSection---wrapper {
    padding: 70px 0 90px;
}

/* Heading fades in from above */
.contactSection---wrapper .heading--wrapper {
    opacity: 0;
    transform: translateY(-20px);
    transition: opacity 0.65s ease, transform 0.65s ease;
}
.active--s .heading--wrapper {
    opacity: 1;
    transform: translateY(0);
}

/* ── Main Layout (2 Columns) ── */
.contact-layout {
    display: flex;
    gap: 48px;
    align-items: flex-start;
    justify-content: space-between;
}

/* ── Left Column ── */
.contact-left {
    flex: 1;
    min-width: 320px;
    position: sticky;
    top: 100px;
    align-self: flex-start;
    opacity: 0;
    transform: translateX(-40px);
    transition: opacity 0.75s 0.15s cubic-bezier(0.22, 1, 0.36, 1), transform 0.75s 0.15s cubic-bezier(0.22, 1, 0.36, 1);
}
.active--s .contact-left {
    opacity: 1;
    transform: translateX(0);
}

.contact-title {
    display: flex;
    flex-direction: column;
    font-family: var(--font-display);
    line-height: 1.25;
    margin-bottom: 20px;
}
.title-top {
    font-size: 26px;
    font-weight: 500;
    color: #ffffff;
    margin-bottom: 6px;
}
.title-gradient {
    font-size: clamp(28px, 3.5vw, 38px);
    font-weight: 700;
    background: linear-gradient(90deg, #6c63ff 0%, #9b59f5 100%);
    -webkit-background-clip: text;
    background-clip: text;
    color: transparent;
}

.contact-desc {
    font-size: 15px;
    color: rgba(255, 255, 255, 0.65);
    line-height: 1.7;
    margin-bottom: 36px;
    max-width: 480px;
}

/* Info Cards List */
.info-list {
    display: flex;
    flex-direction: column;
    gap: 18px;
    margin-bottom: 36px;
}

.info-card {
    display: flex;
    align-items: center;
    gap: 16px;
}

.info-icon {
    width: 44px;
    height: 44px;
    border-radius: 12px;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-shrink: 0;
}
.info-icon svg {
    width: 20px;
    height: 20px;
}

.email-bg {
    color: #3b82f6;
    background: rgba(59, 130, 246, 0.1);
}
.phone-bg {
    color: #06b6d4;
    background: rgba(6, 182, 212, 0.1);
}
.loc-bg {
    color: #10b981;
    background: rgba(16, 185, 129, 0.1);
}

.info-text {
    display: flex;
    flex-direction: column;
}
.info-label {
    font-size: 13px;
    color: rgba(255, 255, 255, 0.5);
    margin-bottom: 2px;
}
.info-val {
    font-size: 15px;
    color: #ffffff;
    font-weight: 500;
}

.optional-txt {
    font-size: 12px;
    color: rgba(255, 255, 255, 0.4);
    font-weight: 400;
    margin-left: 4px;
}

/* Connect & Social Icons */
.connect-wrapper {
    display: flex;
    flex-direction: column;
    gap: 12px;
}
.connect-label {
    font-size: 13px;
    color: rgba(255, 255, 255, 0.5);
}

.social--wrapper {
    display: flex;
    align-items: center;
    gap: 12px;
}
.social-icon {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 42px;
    height: 42px;
    border-radius: 50%;
    color: rgba(255, 255, 255, 0.55);
    border: 1.5px solid rgba(255, 255, 255, 0.12);
    background: rgba(255, 255, 255, 0.03);
    transition: color 0.22s ease, border-color 0.22s ease, background 0.22s ease, box-shadow 0.22s ease, transform 0.22s ease;
}
.social-icon svg {
    width: 19px;
    height: 19px;
}
.social-icon:hover {
    color: #fff;
    border-color: rgba(108, 99, 255, 0.65);
    background: rgba(108, 99, 255, 0.18);
    box-shadow: 0 6px 20px rgba(108, 99, 255, 0.3);
    transform: translateY(-3px);
}

/* ── Right Column: Form Card ── */
.contact-right {
    flex: 1.1;
    min-width: 340px;
}

.form-card {
    background: rgba(18, 17, 43, 0.55);
    border: 1px solid rgba(255, 255, 255, 0.08);
    border-radius: 22px;
    padding: 38px 34px;
    box-shadow: 0 16px 45px rgba(0, 0, 0, 0.45), 0 0 25px rgba(108, 99, 255, 0.12);
    backdrop-filter: blur(12px);
    position: relative;
}

.form {
    display: flex;
    flex-direction: column;
    gap: 20px;
}

.form-row {
    display: flex;
    gap: 16px;
}
.form-row .input-field {
    flex: 1;
}

.input-field {
    display: flex;
    flex-direction: column;
    position: relative;
}

.input-field label {
    font-size: 14px;
    color: rgba(255, 255, 255, 0.85);
    margin-bottom: 8px;
    font-weight: 500;
}

.input-field input,
.input-field textarea {
    width: 100%;
    background: rgba(255, 255, 255, 0.03);
    border: 1px solid rgba(255, 255, 255, 0.09);
    border-radius: 12px;
    padding: 12px 16px;
    color: #ffffff;
    font-family: var(--font-body);
    font-size: 14px;
    outline: none;
    transition: border-color 0.25s ease, background 0.25s ease, box-shadow 0.25s ease;
}

.input-field input::placeholder,
.input-field textarea::placeholder {
    color: rgba(255, 255, 255, 0.35);
}

.input-field input:focus,
.input-field textarea:focus {
    border-color: rgba(108, 99, 255, 0.6);
    background: rgba(108, 99, 255, 0.06);
    box-shadow: 0 0 0 3px rgba(108, 99, 255, 0.15);
}

.form-submit-btn {
    width: 100%;
    padding: 14px;
    font-size: 15px;
    margin-top: 6px;
    border-radius: 12px;
    display: inline-flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
    color: #fff;
    background: linear-gradient(90deg, #6c63ff 0%, #9b59f5 50%, #6c63ff 100%);
    background-size: 200% 100%;
    background-position: left center;
    border: none;
    cursor: pointer;
    box-shadow: 0 4px 20px rgba(108, 99, 255, 0.4);
    transition: background-position 0.55s ease, box-shadow 0.3s ease, transform 0.2s ease;
}
.form-submit-btn:hover {
    background-position: right center;
    box-shadow: 0 8px 28px rgba(155, 89, 245, 0.55);
    transform: translateY(-2px);
}

.btn-icon {
    width: 18px;
    height: 18px;
}

/* Errors & Popups */
.inputError {
    display: none;
    font-size: 12px;
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

.formPopUp {
    display: flex;
    align-items: center;
    gap: 10px;
    padding: 12px 18px;
    border-radius: 12px;
    margin-top: 15px;
    font-size: 14px;
}
.formPopUp--ok {
    background: rgba(16, 185, 129, 0.15);
    border: 1px solid rgba(16, 185, 129, 0.4);
    color: #34d399;
}
.formPopUp--error {
    background: rgba(239, 68, 68, 0.15);
    border: 1px solid rgba(239, 68, 68, 0.4);
    color: #f87171;
}
.popIcon {
    width: 20px;
    height: 20px;
}

/* ── Professional Success Modal Overlay ── */
.modal-overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    background: rgba(8, 7, 20, 0.75);
    backdrop-filter: blur(10px);
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 99999;
    padding: 20px;
}
.modal-card {
    background: #12112b;
    border: 1px solid rgba(108, 99, 255, 0.35);
    border-radius: 24px;
    padding: 40px 36px;
    max-width: 480px;
    width: 100%;
    text-align: center;
    box-shadow: 0 25px 60px rgba(0, 0, 0, 0.6), 0 0 40px rgba(108, 99, 255, 0.25);
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 18px;
}
.modal-icon-glow {
    width: 64px;
    height: 64px;
    border-radius: 50%;
    background: rgba(52, 211, 153, 0.15);
    color: #34d399;
    border: 1px solid rgba(52, 211, 153, 0.4);
    display: flex;
    align-items: center;
    justify-content: center;
    box-shadow: 0 0 25px rgba(52, 211, 153, 0.3);
}
.modal-icon-glow svg {
    width: 32px;
    height: 32px;
}
.modal-title {
    font-family: var(--font-display);
    font-size: 22px;
    font-weight: 700;
    color: #ffffff;
    margin: 0;
}
.modal-desc {
    font-size: 14.5px;
    color: rgba(255, 255, 255, 0.85);
    line-height: 1.65;
    margin: 0;
    direction: rtl;
    text-align: center;
}
.modal-desc-en {
    display: block;
    direction: ltr;
    margin-top: 8px;
    font-size: 13.5px;
    color: rgba(255, 255, 255, 0.6);
}
.modal-close-btn {
    margin-top: 6px;
    width: 140px;
    padding: 10px 0;
    border-radius: 50px;
    font-size: 14px;
}

/* Modal Transition */
.modal-enter-active, .modal-leave-active {
    transition: opacity 0.35s ease, transform 0.35s ease;
}
.modal-enter-from, .modal-leave-to {
    opacity: 0;
    transform: scale(0.92);
}

/* Responsive */
@media screen and (max-width: 900px) {
    .contact-layout {
        flex-direction: column;
        gap: 40px;
    }
    .contact-left, .contact-right {
        width: 100%;
    }
    .form-row {
        flex-direction: column;
        gap: 20px;
    }
}
</style>