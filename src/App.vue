<script setup>
import headerSection from "./components/headerSection/headerSection.vue";
import homeSection from "./components/mainSection/homeSection/homeSection.vue";
import showcaseSection from "./components/mainSection/showcaseSection/showcaseSection.vue";
import contactSection from "./components/mainSection/contactSection/contactSection.vue";
// import footerSection from "./components/footerSection/footerSectoin.vue";
import { onMounted, ref } from "vue";
import AboutMeSection from "./components/mainSection/aboutMeSection/aboutMeSection.vue";
import ServicesSection from "./components/mainSection/servicesSection/servicesSection.vue";


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
        <div class="sections" id="contact">
          <contactSection></contactSection>
        </div>
      </main>

      <footer>
        <!-- <footerSection></footerSection> -->
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
  /* Background Linear — design system */
  background: linear-gradient(135deg, #0a0c1b 0%, #0d0f22 50%, #0a0c1b 100%);
  position: relative;
}
main::before {
  content: '';
  position: absolute;
  inset: 0;
  background:
    radial-gradient(ellipse 80% 60% at 0% 0%, rgba(108, 99, 255, 0.12) 0%, transparent 60%),
    radial-gradient(ellipse 60% 50% at 100% 100%, rgba(155, 89, 245, 0.08) 0%, transparent 60%);
  pointer-events: none;
  z-index: 0;
}
main > * {
  position: relative;
  z-index: 1;
}

</style>
