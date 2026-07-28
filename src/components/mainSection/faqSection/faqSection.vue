<script setup>
import { ref } from 'vue';

const openFaqs = ref([0]); // First one open by default

const faqs = [
    {
        question: "What is your UI/UX design process?",
        answer: "I start with user research and wireframing, create high-fidelity UI designs in Figma, and build interactive prototypes ready for development."
    },
    {
        question: "How long does a design project take?",
        answer: "Landing pages take about 1 to 2 weeks, while full web or mobile applications take 3 to 5 weeks depending on scope."
    },
    {
        question: "What deliverables will I receive?",
        answer: "You get organized Figma source files with design system components, tokens, exportable assets, and interactive prototypes."
    },
    {
        question: "Do you support developers during implementation?",
        answer: "Yes, I provide clear developer specs in Figma and stay available throughout the build to ensure pixel-perfect accuracy."
    },
    {
        question: "Are you open for freelance or full-time roles?",
        answer: "Yes! I am available for freelance projects and remote full-time UI/UX designer positions worldwide."
    }
];

function toggleFaq(index) {
    if (openFaqs.value.includes(index)) {
        openFaqs.value = openFaqs.value.filter(i => i !== index);
    } else {
        openFaqs.value.push(index);
    }
}
</script>

<template>
    <div class="faqSection--wrapper" id="faq">
        <div class="container">

            <!-- Heading -->
            <div class="heading--wrapper">
                <h2 class="heading">FAQ</h2>
            </div>

            <!-- FAQ Accordion Container -->
            <div class="faq-accordion-list">
                <div
                    v-for="(faq, index) in faqs"
                    :key="index"
                    class="faq-card"
                    :class="{ 'is-open': openFaqs.includes(index) }"
                    @click="toggleFaq(index)"
                >
                    <div class="faq-header">
                        <h3 class="faq-question">{{ faq.question }}</h3>
                        <div class="faq-toggle-icon">
                            <div class="horizontal-line"></div>
                            <div class="vertical-line"></div>
                        </div>
                    </div>

                    <div class="faq-body">
                        <div class="faq-content">
                            <p>{{ faq.answer }}</p>
                        </div>
                    </div>
                </div>
            </div>

        </div>
    </div>
</template>

<style scoped>
.faqSection--wrapper {
    padding: 90px 0;
    position: relative;
}

.heading--wrapper {
    text-align: center;
    margin-bottom: 50px;
    opacity: 0;
    transform: translateY(-24px);
    transition: opacity 0.8s cubic-bezier(0.22, 1, 0.36, 1), transform 0.8s cubic-bezier(0.22, 1, 0.36, 1);
}
.active--s .heading--wrapper {
    opacity: 1;
    transform: translateY(0);
}


/* Accordion List */
.faq-accordion-list {
    max-width: 820px;
    margin: 0 auto;
    display: flex;
    flex-direction: column;
    gap: 16px;
    opacity: 0;
    transform: translateY(30px);
    transition: opacity 0.85s 0.15s cubic-bezier(0.22, 1, 0.36, 1), transform 0.85s 0.15s cubic-bezier(0.22, 1, 0.36, 1);
}
.active--s .faq-accordion-list {
    opacity: 1;
    transform: translateY(0);
}

/* Single FAQ Card */
.faq-card {
    background: rgba(18, 17, 43, 0.5);
    border: 1px solid rgba(255, 255, 255, 0.08);
    border-radius: 18px;
    padding: 22px 28px;
    backdrop-filter: blur(12px);
    cursor: pointer;
    transition: background 0.3s ease, border-color 0.3s ease, box-shadow 0.3s ease, transform 0.25s ease;
    overflow: hidden;
}
.faq-card:hover {
    background: rgba(24, 22, 56, 0.65);
    border-color: rgba(108, 99, 255, 0.35);
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3), 0 0 15px rgba(108, 99, 255, 0.1);
    transform: translateY(-2px);
}
.faq-card.is-open {
    background: rgba(26, 23, 60, 0.75);
    border-color: rgba(108, 99, 255, 0.45);
    box-shadow: 0 14px 40px rgba(0, 0, 0, 0.4), 0 0 20px rgba(108, 99, 255, 0.15);
}

/* Header */
.faq-header {
    display: flex;
    align-items: center;
    gap: 16px;
    user-select: none;
}
.faq-question {
    font-family: var(--font-display);
    font-size: 16.5px;
    font-weight: 500;
    color: rgba(255, 255, 255, 0.9);
    margin: 0;
    flex: 1;
    line-height: 1.4;
    transition: color 0.25s ease;
}
.faq-card:hover .faq-question,
.faq-card.is-open .faq-question {
    color: #ffffff;
}

.faq-toggle-icon {
    position: relative;
    width: 18px;
    height: 18px;
    flex-shrink: 0;
}
.faq-toggle-icon .horizontal-line,
.faq-toggle-icon .vertical-line {
    position: absolute;
    background: linear-gradient(90deg, #6c63ff 0%, #9b59f5 100%);
    border-radius: 4px;
    transition: transform 0.35s cubic-bezier(0.22, 1, 0.36, 1), opacity 0.3s ease;
}
.faq-toggle-icon .horizontal-line {
    top: 50%;
    left: 0;
    width: 100%;
    height: 2px;
    transform: translateY(-50%);
}
.faq-toggle-icon .vertical-line {
    top: 0;
    left: 50%;
    width: 2px;
    height: 100%;
    transform: translateX(-50%);
}

.faq-card.is-open .faq-toggle-icon .vertical-line {
    transform: translateX(-50%) rotate(90deg);
    opacity: 0;
}
.faq-card.is-open .faq-toggle-icon .horizontal-line {
    transform: translateY(-50%) scale(1.1);
}

/* Accordion Smooth Body Expansion */
.faq-body {
    max-height: 0;
    overflow: hidden;
    opacity: 0;
    transition: max-height 0.45s cubic-bezier(0.25, 1, 0.5, 1), opacity 0.4s ease;
    will-change: max-height, opacity;
}
.faq-card.is-open .faq-body {
    max-height: 180px;
    opacity: 1;
    transition: max-height 0.48s cubic-bezier(0.25, 1, 0.5, 1), opacity 0.45s ease;
}
.faq-content p {
    font-size: 14px;
    color: rgba(255, 255, 255, 0.68);
    line-height: 1.65;
    margin: 14px 0 2px 0;
    border-top: 1px solid rgba(255, 255, 255, 0.06);
    padding-top: 14px;
}

/* Responsive */
@media screen and (max-width: 768px) {
    .faqSection--wrapper {
        padding: 60px 0;
    }
    .faq-card {
        padding: 18px 20px;
    }
    .faq-question {
        font-size: 15px;
    }
    .faq-content p {
        margin-left: 0;
        font-size: 13.5px;
    }
}
</style>
