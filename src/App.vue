<script setup>
import { onMounted, ref, defineAsyncComponent } from "vue";
import headerSection from "./components/headerSection/headerSection.vue";
import homeSection from "./components/mainSection/homeSection/homeSection.vue";
import { Analytics } from '@vercel/analytics/vue';
import { SpeedInsights } from '@vercel/speed-insights/vue';

// Code-split below-the-fold components for faster FCP/LCP
const CustomCursor = defineAsyncComponent(() => import("./components/CustomCursor.vue"));
const AboutMeSection = defineAsyncComponent(() => import("./components/mainSection/aboutMeSection/aboutMeSection.vue"));
const ServicesSection = defineAsyncComponent(() => import("./components/mainSection/servicesSection/servicesSection.vue"));
const showcaseSection = defineAsyncComponent(() => import("./components/mainSection/showcaseSection/showcaseSection.vue"));
const ProcessSection = defineAsyncComponent(() => import("./components/mainSection/processSection/processSection.vue"));
const contactSection = defineAsyncComponent(() => import("./components/mainSection/contactSection/contactSection.vue"));
const FaqSection = defineAsyncComponent(() => import("./components/mainSection/faqSection/faqSection.vue"));
const footerSection = defineAsyncComponent(() => import("./components/footerSection/footerSection.vue"));


if (window.location.hash) {
  const urlWithoutHash = window.location.origin + window.location.pathname + window.location.search;
  window.location.href = urlWithoutHash;
}

const sections = ref();
const whitchMenuActive = ref();
const Observer = new IntersectionObserver((entries)=> {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      entry.target.classList.add('active--s');
      const activeSection = ref(entry.target.getAttribute('id'));
      whitchMenuActive.value = activeSection.value;
    }
  });
}, {
  rootMargin: '-45% 0px -45% 0px'
});

onMounted(()=> {

  sections.value = document.querySelectorAll('.sections');
  sections.value.forEach((section)=> {
    Observer.observe(section);
  });


});


</script>

<template>

  <div class="wrapper">
    <CustomCursor />


    <div class="homeAndHeader">
      <header>
        <headerSection :whitchMenuActive="whitchMenuActive"></headerSection>
      </header>

      <div class="sections" id="home">
        <homeSection></homeSection>
      </div>
    </div>


    <!-- <div class="container"> -->
  
      <main>
        <div class="sections" id="aboutMe">
          <AboutMeSection></AboutMeSection>
        </div>
        <div class="sections" id="services">
          <ServicesSection></ServicesSection>
        </div>
        <div class="sections" id="Portfolio">
          <showcaseSection></showcaseSection>
        </div>
        <div class="sections" id="process">
          <ProcessSection></ProcessSection>
        </div>
        <div class="sections" id="contact">
          <contactSection></contactSection>
        </div>
        <div class="sections" id="faq">
          <FaqSection></FaqSection>
        </div>
      </main>

      <footer>
        <footerSection></footerSection>
      </footer>

    <!-- </div> -->
  </div>
  <Analytics />
  <SpeedInsights />

</template>

<style>

.wrapper {
  width: 100%;
  overflow-x: hidden;
  position: relative;
}

header {
  width: 100%;
  position: fixed;
  top: 0; 
  left: 0;
  z-index: 100;
}

.homeAndHeader {
  width: 100%;
  overflow: hidden;
  background-color: var(--bg-dark);
  background-image:
    radial-gradient(ellipse 60% 55% at 50% 48%, rgba(108, 99, 255, 0.22) 0%, rgba(108, 99, 255, 0.06) 55%, transparent 100%),
    radial-gradient(ellipse 100% 40% at 50% 0%, rgba(80, 60, 200, 0.12) 0%, transparent 70%);
  position: relative;
}

#home {
  min-height: 100vh;
  height: auto;
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  padding: 120px 0 80px;
}

@media screen and (max-width: 991px) {
  .homeAndHeader {
    background-image:
      radial-gradient(ellipse 100% 35% at 50% 0%, rgba(80, 60, 200, 0.12) 0%, transparent 70%);
  }
  #home {
    height: auto;
    min-height: auto;
    padding: 144px 0 72px;
  }
}

@media screen and (max-width: 768px) {
  #home {
    padding: 140px 0 64px;
  }
}

@media screen and (max-width: 480px) {
  #home {
    padding: 136px 0 56px;
  }
}
main {
  /* Rich deep background — brand accent dark tones */
  background:
    linear-gradient(135deg, #070a18 0%, #0c0e20 40%, #0f0a1e 70%, #080a18 100%);
  position: relative;
  overflow: hidden;
}

/* Multi-layer ambient glow overlay */
main::before {
  content: '';
  position: absolute;
  inset: 0;
  background:
    /* Top-left large indigo bloom */
    radial-gradient(ellipse 70% 45% at -5% 5%,  rgba(108, 99, 255, 0.18) 0%, transparent 65%),
    /* Bottom-right violet accent */
    radial-gradient(ellipse 60% 40% at 105% 95%, rgba(155, 89, 245, 0.14) 0%, transparent 60%),
    /* Center-top soft haze */
    radial-gradient(ellipse 90% 30% at 50% 0%,  rgba(80, 60, 200, 0.10) 0%, transparent 70%),
    /* Mid-left subtle glow */
    radial-gradient(ellipse 40% 35% at 0% 55%,  rgba(108, 99, 255, 0.08) 0%, transparent 60%),
    /* Bottom-center cool violet breath */
    radial-gradient(ellipse 75% 25% at 50% 100%, rgba(120, 80, 255, 0.10) 0%, transparent 65%);
  pointer-events: none;
  z-index: 0;
}

/* Subtle diagonal accent stripe */
main::after {
  content: '';
  position: absolute;
  inset: 0;
  background:
    linear-gradient(115deg,
      rgba(108, 99, 255, 0.04) 0%,
      transparent 35%,
      transparent 65%,
      rgba(155, 89, 245, 0.05) 100%
    );
  pointer-events: none;
  z-index: 0;
}

main > * {
  position: relative;
  z-index: 1;
}

</style>
