<script setup>
import headerSection from "./components/headerSection/headerSection.vue";
import homeSection from "./components/mainSection/homeSection/homeSection.vue";
import showcaseSection from "./components/mainSection/showcaseSection/showcaseSection.vue";
import contactSection from "./components/mainSection/contactSection/contactSection.vue";
import ProcessSection from "./components/mainSection/processSection/processSection.vue";
import footerSection from "./components/footerSection/footerSection.vue";
import { onMounted, ref } from "vue";
import AboutMeSection from "./components/mainSection/aboutMeSection/aboutMeSection.vue";
import ServicesSection from "./components/mainSection/servicesSection/servicesSection.vue";
import CustomCursor from "./components/CustomCursor.vue";
import FaqSection from "./components/mainSection/faqSection/faqSection.vue";


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

</template>

<style>

header {
  width: 100%;
  position: fixed;
  top: 0; 
  left: 0;
  z-index: 100;
}

.homeAndHeader {
  width: 100%;
  background-color: var(--bg-dark);
  /* Figma IDM background: dark navy + centered blurred purple glow circle */
  background-image:
    radial-gradient(ellipse 60% 55% at 50% 48%, rgba(108, 99, 255, 0.22) 0%, rgba(108, 99, 255, 0.06) 55%, transparent 100%),
    radial-gradient(ellipse 100% 40% at 50% 0%, rgba(80, 60, 200, 0.12) 0%, transparent 70%);
  position: relative;
}

#home {
  height: 100vh;
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  padding: 75px 25px;
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
