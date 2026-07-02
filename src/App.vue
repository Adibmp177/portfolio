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
  background-image: url(./assets/homeImage/home-bg.webp);
  background-position: center;
  background-size: cover;
  width: 100%;
}

#home {
  height: 100vh;
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  background-color: rgba(0, 0, 0, 0.5);
  padding: 75px 25px;
}
main {
  background: radial-gradient(69.9% 149.37% at -7.92% -4.45%, rgba(20, 38, 205, 0.23) 0%, rgba(20, 38, 205, 0.155) 100%), radial-gradient(75.56% 161.46% at -13.58% -6.36%, rgba(233, 30, 30, 0.329) 0%, rgba(233, 30, 30, 0.007) 100%);
}

</style>
