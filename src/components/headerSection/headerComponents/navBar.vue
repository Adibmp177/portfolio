<script setup>
import { defineProps, defineEmits, ref, watch } from 'vue';
import ResumeButton from './resumeButton.vue';
import { onMounted } from 'vue';
const props = defineProps(['menuHandler', 'whitchMenuActive']); 
const emits = defineEmits(['toggleMenu','toResume']); 

const menuData = ref([
    {
        id: 1,
        menu: "home",
        anckorLink: "home",
    },
    {
        id: 2,
        menu: "about me",
        anckorLink: "aboutMe",
    },
    {
        id: 3,
        menu: "services",
        anckorLink: "services",
    },
    {
        id: 4,
        menu: "Portfolio",
        anckorLink: "Portfolio",
    },
    {
        id: 5,
        menu: "contact",
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
    } else {
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
    firstMenuActive.parentElement.style.setProperty("--transformXJS", `${firstMenuActive.offsetLeft}px`);
    firstMenuActive.parentElement.style.setProperty("--widthJS", `${firstMenuActive.offsetWidth}px`);
    
    // activeingMenu(whitchMenuActive.value, false, activeMenu.value[0]);

    window.addEventListener("resize", ()=> {
        
        if (window.innerWidth >= 991) {
            let item = document.querySelector(".menuItems.activeMenu");
            
            item.parentElement.style.setProperty("--transformXJS", `${item.offsetLeft}px`);
            item.parentElement.style.setProperty("--widthJS", `${item.offsetWidth}px`);
        }
    });
})

watch(()=> props.whitchMenuActive, (newValue) => {
    console.log(props.whitchMenuActive);
    
    if (isWatching.value) {
        console.log(props.whitchMenuActive+"log-2");
        let item;   
        activeMenu.value.forEach(el => {
            el.classList.contains("activeMenu") && el.classList.remove("activeMenu");
            if (el.firstElementChild.getAttribute("href").slice(1) === newValue) {
                el.classList.add("activeMenu");
                item = el;
            }
        });
        menuHandler(newValue, true, props.menuHandler, item);
        
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
    bottom: 0;
    transform: translateX(var(--transformXJS));
    width: var(--widthJS);
    height: 2px;
    background: var(--bg-gradient-linear);
    transition: 0.5s linear;
}

.menuItems {
    position: relative;
    color: var(--main-txt);
    transition: 0.3s;
} 
.menuItems a {
    cursor: pointer;
    text-transform: capitalize;
    font-size: 18px;
    padding: 0 20px;
    font-weight: 500;
    font-family: bayer;
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

@media screen and (max-width: 991px) {
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
        position: absolute;
        left: 50%;
        bottom: 10px;
        transform: translate(-50%, 100%);
        border: 2px solid rgba(216, 216, 216, 0.4);
        width: 98%;
        border-radius: 15px 15px;
        overflow: hidden;
        height: auto;
        visibility: hidden;
        opacity: 0;
        transition: 0.5s;
        padding: 40px 0 20px;
        background-color: rgba(0, 0, 0, 0.95);
        z-index: 9999;
    }
    .active {
        visibility: visible;
        opacity: 1;
        bottom: -25px;
    }
    .menu--container {
        flex-direction: column;
        justify-content: center;
        align-items: center;
        gap: 40px 0;
        width: 100%;
        
    }
    .menuItems a {
        display: block;
        padding: 0 20px;
    }
    .resumeButton-wrapper {
        display: flex;
        justify-content: center;
        margin: 35px 0 15px; 
    }
}

</style>