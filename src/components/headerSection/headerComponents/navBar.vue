<script setup>
import { defineProps, defineEmits, ref, watch } from 'vue';
import ResumeButton from './resumeButton.vue';
import { onMounted } from 'vue';
const props = defineProps(['menuHandler', 'whitchMenuActive']); 
const emits = defineEmits(['toggleMenu','toResume']); 

const menuData = ref([
    {
        id: 1,
        menu: "Home",
        anckorLink: "home",
    },
    {
        id: 2,
        menu: "About",
        anckorLink: "aboutMe",
    },
    {
        id: 3,
        menu: "Projects",
        anckorLink: "Portfolio",
    },
    {
        id: 4,
        menu: "Process",
        anckorLink: "process",
    },
    {
        id: 5,
        menu: "Contact",
        anckorLink: "contact",
    },
]);

const whitchMenuActive = ref('home');
const isWatching = ref(true); // handel watch when user click on menu Items




function menuHandler(newValu, isInWatch, isMenuOpen, item) {
    whitchMenuActive.value = newValu;
    if (window.innerWidth <= 991) {

        if (isInWatch) {
            if (isMenuOpen) {
                setTimeout(() => {
                    emits('toggleMenu');
                    console.log("Hiiiiiiiiiiii Im here :) (1)");
                }, 500); 
            }
        } else if (!isInWatch && !isMenuOpen) {
            console.log("Hiiiiiiiiiiii Im here :) (2)");
        } else {
            setTimeout(() => {
                emits('toggleMenu');
                console.log("Hiiiiiiiiiiii Im here :) (3)");
                isWatching.value = true;
            }, 500);
        }
    } else if (item && item.parentElement) {
        item.parentElement.style.setProperty("--transformXJS", `${item.offsetLeft}px`);
        item.parentElement.style.setProperty("--widthJS", `${item.offsetWidth}px`);
        if (!isInWatch) {
            setTimeout(() => {
                isWatching.value = true;
                console.log("Hiiiiiiiiiiii Im here :) (4)");
            }, 500);
        }
    }
    
}

let activeMenu = ref();
onMounted(()=> {
    activeMenu.value = document.querySelectorAll(".menuItems");

    let firstMenuActive = document.querySelector(".menuItems.activeMenu");
    if (firstMenuActive && firstMenuActive.parentElement) {
        firstMenuActive.parentElement.style.setProperty("--transformXJS", `${firstMenuActive.offsetLeft}px`);
        firstMenuActive.parentElement.style.setProperty("--widthJS", `${firstMenuActive.offsetWidth}px`);
    }
    
    // activeingMenu(whitchMenuActive.value, false, activeMenu.value[0]);

    window.addEventListener("resize", ()=> {
        
        if (window.innerWidth >= 991) {
            let item = document.querySelector(".menuItems.activeMenu");
            if (item && item.parentElement) {
                item.parentElement.style.setProperty("--transformXJS", `${item.offsetLeft}px`);
                item.parentElement.style.setProperty("--widthJS", `${item.offsetWidth}px`);
            }
        }
    });
})

watch(()=> props.whitchMenuActive, (newValue) => {
    console.log(props.whitchMenuActive);
    
    if (isWatching.value) {
        console.log(props.whitchMenuActive+"log-2");
        let item = null;   
        if (activeMenu.value) {
            activeMenu.value.forEach(el => {
                if (el.firstElementChild && el.firstElementChild.getAttribute("href")) {
                    const href = el.firstElementChild.getAttribute("href").slice(1);
                    if (href === newValue) {
                        el.classList.add("activeMenu");
                        item = el;
                    } else {
                        el.classList.remove("activeMenu");
                    }
                }
            });
        }
        if (item) {
            menuHandler(newValue, true, props.menuHandler, item);
        }
        
        console.log("Hi ferey we are Here, in watch");
    }
}, { immediate: false });


function activeingMenu(menu, isClickedOrNot, item) {
    
    
    document.querySelector(".menuItems.activeMenu").classList.remove("activeMenu");
    item.classList.add("activeMenu");

    isWatching.value = false;
    menuHandler(menu, isWatching.value, isClickedOrNot, item);
}





    
function openResume() {
    emits('toResume');
}

</script>

<template>

    <!-- Mobile Menu Backdrop Overlay -->
    <div class="mobile-menu-overlay" :class="{'is-visible': props.menuHandler}" @click="emits('toggleMenu')"></div>

    <div class="menu--wrapper" :class="{'active': props.menuHandler}">

        <div class="menu--container">

            <div 
                class="menuItems" 
                :class="{'activeMenu': whitchMenuActive === item.anckorLink}" 
                v-for="item in menuData" 
                :key="item.id"
                >
                
                <a :href="`#${item.anckorLink}`" @click="activeingMenu(item.anckorLink, true, $event.currentTarget.parentElement)">
                    {{ item.menu }}
                </a>
            </div>

            
        </div>
        <div class="resumeButton-wrapper" @click="openResume">
            <ResumeButton></ResumeButton>
        </div>

    </div>
    

</template>

<style scoped>



.resumeButton-wrapper {
    display: none;
}

.menu--wrapper {
    opacity: 1;
    transform: translateX(0px);
    /* interpolate-size: allow-keywords; */
} 

.menu--container {
    display: flex;
    align-items: center;
    gap: 0 10px;
    position: relative;
    transition: 0.35s;

}
.menu--container::after {
    content: "";
    position: absolute;
    bottom: -6px;
    left: 0;
    transform: translateX(var(--transformXJS, 0px));
    width: var(--widthJS, 0px);
    height: 3px;
    border-radius: 2px;
    background: linear-gradient(90deg, #6c63ff 0%, #9b59f5 100%);
    transition: transform 0.38s cubic-bezier(0.25, 1, 0.5, 1), width 0.38s cubic-bezier(0.25, 1, 0.5, 1);
    box-shadow: 0 2px 12px rgba(108, 99, 255, 0.6);
}

.menuItems {
    position: relative;
    color: var(--main-txt);
    transition: 0.3s;
} 
.menuItems a {
    cursor: pointer;
    text-transform: capitalize;
    font-size: 15px;
    padding: 0 14px;
    font-weight: 500;
    font-family: var(--font-body);
    height: 100%;
}
.menuItems::after {
    content: "";
    position: absolute;
    width: 50%;
    height: 3px;
    bottom: -15px;
    left: 50%;
    transform: translateX(-50%);
    opacity: 0;
    background: var(--bg-gradient-linear);
    transition: 0.35;
}
/* .menuItems:hover {
    transition: 0.3s;
}
.menuItems:hover::after {
    transition: 0.5s;
    width: 80%;
    opacity: 1;
    bottom: -5px;
} */




.disabled, .disabled a{
    opacity: 0.6;
    cursor: not-allowed;
}

.mobile-menu-overlay {
    display: none;
}

@media screen and (max-width: 991px) {
    .mobile-menu-overlay {
        display: block;
        position: fixed;
        top: 0;
        left: 0;
        width: 100vw;
        height: 100vh;
        background: rgba(4, 3, 15, 0.45);
        backdrop-filter: blur(10px);
        -webkit-backdrop-filter: blur(10px);
        z-index: 9998;
        opacity: 0;
        visibility: hidden;
        transition: opacity 0.4s ease, visibility 0.4s ease;
    }
    .mobile-menu-overlay.is-visible {
        opacity: 1;
        visibility: visible;
    }

    .menu--container::after {
        display: none;
    }
    .activeMenu.menuItems::after {
        width: 80%;
        opacity: 1;
        bottom: -5px;
    }
    .menu--wrapper {
        animation: unset;
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        border: none;
        border-bottom: 1px solid rgba(108, 99, 255, 0.25);
        border-radius: 0 0 24px 24px;
        overflow: hidden;
        height: auto;
        visibility: hidden;
        opacity: 0;
        transform: translateY(-20px);
        transition: 0.4s cubic-bezier(0.22, 1, 0.36, 1);
        padding: 100px 0 30px; /* Space for the header elements */
        background: rgba(12, 10, 32, 0.97);
        backdrop-filter: blur(24px);
        -webkit-backdrop-filter: blur(24px);
        box-shadow: 0 20px 50px rgba(0, 0, 0, 0.7);
        z-index: 9999;
    }
    .active {
        visibility: visible;
        opacity: 1;
        transform: translateY(0);
    }
    .menu--container {
        flex-direction: column;
        justify-content: center;
        align-items: center;
        gap: 32px 0;
        width: 100%;
    }
    .menuItems a {
        display: block;
        font-size: 18px;
        font-weight: 500;
        padding: 4px 20px;
        letter-spacing: 0.3px;
    }
    .resumeButton-wrapper {
        display: flex;
        justify-content: center;
        margin: 32px 0 10px;
    }
}

</style>