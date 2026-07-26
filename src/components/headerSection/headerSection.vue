<script setup>
import navBar from "./headerComponents/navBar.vue";
import hamburgerMenu from "./headerComponents/hamburgerMenu.vue";
import resumeButton from "./headerComponents/resumeButton.vue";
import { ref, defineProps, onMounted, defineEmits } from "vue";

const props = defineProps(['whitchMenuActive']);
const emits = defineEmits(['headerContainerHandler']);

const menuHandler = ref(false);
function togglingMenu() {
    menuHandler.value = !menuHandler.value;
}

window.addEventListener('resize', ()=> {
    // console.log(window.innerWidth);
    if (window.innerWidth >= 991 && menuHandler.value) {
        // menuHandler.value = false;
        togglingMenu();
    }
})


const ResumeHandler = ref(false);
function openResume() {
    ResumeHandler.value = true;
    document.querySelector('body').style.overflowY = "hidden";
    menuHandler.value = false
    if (menuHandler.value) {
        setTimeout(() => {
        }, 500);
    }
} 
function closeResume() {
    ResumeHandler.value = false;
    document.querySelector('body').style.overflowY = "auto";
}



const stickyMenuHandler = ref(false);
onMounted(() => {
    window.addEventListener("scroll", ()=> {
        
        if (window.scrollY > 100) {
            stickyMenuHandler.value = true;
            emits('headerContainerHandler', true);
        } else {
            stickyMenuHandler.value = false;
            emits('headerContainerHandler', false);
        }
    })
})


</script>

<template>

    <div class="header--wrapper" :class="{'toTop': stickyMenuHandler}">
        <div class="container">
            <a href="#home" class="logoSection">
                <img src="./../../../public/logo/LOGO.png" alt="my personal logo" class="logoImg">
            </a>
    
            <hamburgerMenu @toggleMenu="togglingMenu" :menuHandler="menuHandler"></hamburgerMenu>
    
            <navBar :menuHandler="menuHandler" @to-resume="openResume" @toggle-menu="togglingMenu" :whitchMenuActive="props.whitchMenuActive"></navBar>
    
            <div class="resumeButton--wrapper" @click="openResume">
                <resumeButton></resumeButton>
            </div>
        </div>

    </div>

    <Transition name="fadeResume">
        <div class="resume--wrapper" v-if="ResumeHandler">
            <div class="resume--header">
                <div class="resume-container container rch">
                    <div class="logoBox">
                        <img src="../../../public/logo/LOGO.png" alt="logo" class="logoImg">
                    </div>
                    <div class="x--btn" @click="closeResume" aria-label="Close resume overlay">
                        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor" class="x-b">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M6 18 18 6M6 6l12 12" />
                        </svg>
                    </div>
                </div>
            </div>
            <div class="resume-container container">
                <div class="mainResumes">
                    <div class="resume en-R">
                        <h2 class="resheading">English Resume</h2>
                        <div class="resImgBox">
                            <img loading="lazy" src="../../assets/resumeImg/65afa8c554210e53dbfb7c18_Resume English.png" alt="resume">
                            <a href="/resumes/ResumeEnglish.pdf" download class="downloadResume--btn">
                                <button class="download--btn">
                                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="downloadIcon">
                                        <path stroke-linecap="round" stroke-linejoin="round" d="M3 16.5v2.25A2.25 2.25 0 0 0 5.25 21h13.5A2.25 2.25 0 0 0 21 18.75V16.5M16.5 12 12 16.5m0 0L7.5 12m4.5 4.5V3" />
                                    </svg>
                                    Download English Resume
                                </button>
                            </a>
                        </div>
                    </div>
                    <div class="resume fa-R">
                        <h2 class="resheading">Persian Resume</h2>
                        <div class="resImgBox">
                            <img loading="lazy" src="../../assets/resumeImg/65afa9172d0b012eaed1ede3_Resume Persian.png" alt="resume">
                            <a href="/resumes/ResumePersian.pdf" download class="downloadResume--btn">
                                <button class="download--btn">
                                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="downloadIcon">
                                        <path stroke-linecap="round" stroke-linejoin="round" d="M3 16.5v2.25A2.25 2.25 0 0 0 5.25 21h13.5A2.25 2.25 0 0 0 21 18.75V16.5M16.5 12 12 16.5m0 0L7.5 12m4.5 4.5V3" />
                                    </svg>
                                    Download Persian Resume
                                </button>
                            </a>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </Transition>

</template>

<style scoped>
/* ── Download Resume Button ── */
.downloadResume--btn {
    display: block;
    width: 100%;
}
.download--btn {
    width: 100%;
    color: #fff;
    border: none;
    border-radius: 50px;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 9px;
    font-family: var(--font-body);
    font-size: 15px;
    font-weight: 500;
    letter-spacing: 0.3px;
    cursor: pointer;
    padding: 11px 24px;
    /* Sweep hover: oversized gradient shifts on hover */
    background: linear-gradient(90deg, #6c63ff 0%, #9b59f5 50%, #6c63ff 100%);
    background-size: 200% 100%;
    background-position: left center;
    box-shadow: 0 4px 18px rgba(108, 99, 255, 0.35);
    transition:
        background-position 0.55s ease,
        box-shadow          0.3s ease,
        transform           0.2s ease;
}
.download--btn:hover {
    background-position: right center;
    transform: translateY(-2px);
    box-shadow: 0 10px 28px rgba(155, 89, 245, 0.5);
}
.download--btn:active {
    transform: translateY(1px) scale(0.97);
    box-shadow: 0 3px 12px rgba(108, 99, 255, 0.3);
}
.downloadIcon {
    width: 20px;
    height: 20px;
    flex-shrink: 0;
}

.logoSection {
    display: block;
    cursor: pointer;
}

.fadeResume-enter-active {
  transition: opacity 0.5s ease;
}
.fadeResume-leave-active {
  transition: opacity 0.3s ease;
}

.fadeResume-enter-from,
.fadeResume-leave-to {
  opacity: 0;
}

.header--wrapper {
    width: 100%;
    padding: 20px 0 0px;
    backdrop-filter: blur(0px);
    transition: 0.5s;
}
.header--wrapper .container {
    display: flex;
    justify-content: space-between;
    align-items: center;
}
.toTop {
    background-color: rgba(0, 0, 0, 0.8);
    backdrop-filter: blur(10px);
    padding: 0px 0 0;
}


.logoImg {
    width: 150px;
    transition: width 0.35s;
}
.toTop .logoImg {
    width: 125px;
}

.resume--wrapper {
    position: fixed;
    top: 0;
    left: 0;
    z-index: 10;
    width: 100%;
    height: 100vh;
    overflow-y: scroll;
    overflow-x: hidden;
    background: rgba(10, 12, 27, 0.96);
    backdrop-filter: blur(22px);
    padding: 150px 0;
}

.resume--header {
    width: 100%;
    max-width: 100%;
    position: fixed;
    /* background: #000; */
    z-index: 1;
    top: 0;
    left: 0;
}
/* .resume-container {
    width: 950px;
    max-width: 950px;
    margin: 0 auto;
} */
.rch {
    padding: 17px 0px 10px;
    /* background-color:#333; */
    display: flex;
    align-items: center;
    justify-content: space-between;
}
.logoBox {
    opacity: 0;
    transform: scale(0);
    animation: showL 0.8s 0.3s ease-out forwards;
} @keyframes showL {
    0% {
        opacity: 0;
        transform: scale(0);
    }
    50% {
        opacity: .5;
        transform: scale(1.2);
    }
    100% {
        opacity: 1;
        transform: scale(1);
    }
}

.x--btn {
    width: 45px;
    height: 45px;
    display: flex;
    padding: 5px;
    align-items: center;
    justify-content: center;
    border-radius: 50%;
    color: #fff;
    cursor: pointer;
    /* Sweep animation — same pattern as Fill buttons */
    background: linear-gradient(90deg, #6c63ff 0%, #9b59f5 50%, #6c63ff 100%);
    background-size: 200% 100%;
    background-position: left center;
    box-shadow: 0 4px 18px rgba(108, 99, 255, 0.4);
    opacity: 0;
    transform: scale(0);
    animation: showL 0.35s 0.3s ease-in-out forwards;
    transition:
        background-position 0.55s ease,
        box-shadow          0.3s ease,
        transform           0.22s ease;
}
.x--btn:hover {
    background-position: right center;
    transform: scale(1.08);
    box-shadow: 0 8px 24px rgba(155, 89, 245, 0.55);
}
.x-b {
    width: 22px;
    height: 22px;
}

.mainResumes {
    display: flex;
    justify-content: space-between;
    text-align: center;
    color: #fff;
}
.resume {
    flex: 50%;
    max-width: 50%;
    padding: 0 25px;
}

.en-R {
    opacity: 0;
    transform: translateY(75px);
    animation: showResemesEn 0.7s ease-out 0.5s forwards;
}
@keyframes showResemesEn {
    0% {
        opacity: 0;
        transform: translateY(75px);
    } 
    100% {
        opacity: 1;
        transform: translateY(0);
    }
}
.fa-R {
    opacity: 0;
    transform: translateY(75px);
    animation: showResemesFa 0.7s ease-out 0.5s forwards;
}
@keyframes showResemesFa {
    0% {
        opacity: 0;
        transform: translateY(-75px);
    } 
    100% {
        opacity: 1;
        transform: translateY(0);
    }
}

.resheading {
    margin-bottom: 35px;
}
.resImgBox img {
    width: 100%;
    border-radius: 8px;
}

@media screen and (max-width: 991px) {
    .resumeButton--wrapper {
        display: none;
    }
}

@media screen and (max-width: 960px)  {
    .resume-container {
        width: auto;
        max-width: 950px;
        padding: 0 25px;
    }
}

@media screen and (max-width: 768px) {
  .logoImg {
    width: 125px;
  }
  .mainResumes {
        flex-direction: column;
        justify-content: center;
        gap: 100px;
    }
    .resume {
        flex: 100%;
        max-width: 100%;
        padding: 0 25px;
    }
    .rch {
        padding: 15px 20px;
    }
}
@media screen and (max-width: 450px) {
    .resume {
        padding: 0px;
    }
    .rch {
        padding: 8px 8px 8px 15px;
    }
    .x--btn:hover {
        background-color: unset;
        color: #a1a1a1;
    }
}

</style>