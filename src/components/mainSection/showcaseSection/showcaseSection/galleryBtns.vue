<script setup>
import { ref, defineEmits, onMounted } from "vue";

const emits = defineEmits(["filterGallery"]);

const activeBtn = ref('all');
const gallerBtnsData = ref([
    {
        btnID: 1,
        category: "all",
        btnTitle: "All",
    },
    {
        btnID: 2,
        category: "web",
        btnTitle: "Web Design",
    },
    {
        btnID: 3,
        category: "app",
        btnTitle: "App Design",
    },
    {
        btnID: 4,
        category: "GraphicDesign",
        btnTitle: "Graphic Design",
    },
]);

const btns = ref();
onMounted(()=> {

    btns.value = document.querySelectorAll('.tabsItem');
    setTimeout(() => {
        setActiveIndcator(btns.value[0]);    
    }, 510);

    window.addEventListener('resize', ()=> {
        let activeTab = document.querySelector('.tabsItem.activeTab');
        setActiveIndcator(activeTab);
    })
    
})

function setActiveIndcator(btnItem) {
  btnItem.parentElement.style.setProperty("--transform2JS", `${btnItem.offsetLeft}px`);
  btnItem.parentElement.style.setProperty("--widthJS2", `${btnItem.offsetWidth}px`);
}

function fillterGallery(category, btn) {
    activeBtn.value = category;
    setActiveIndcator(btn);
    emits('filterGallery', category);
    console.log(btn);
}

</script>

<template>

    <div class="tabs--wrapper">
        <div 
            class="tabsItem" 
            v-for="btn in gallerBtnsData" 
            :key="btn.btnID" 
            :class="{ 'activeTab': activeBtn == btn.category }"
            @click="fillterGallery(btn.category, $event.currentTarget)"
            >
            {{ btn.btnTitle }}
        </div>
    </div>

</template>

<style scoped>

.tabs--wrapper {
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 0 25px;
    color: #fff;
    margin-bottom: 35px;
    position: relative;
    overflow: hidden;
} .tabs--wrapper:before {
    content: "";
    position: absolute;
    top: 50%;
    left: 0;
    opacity: 0;
    height: 100%;
    border-radius: 10px;
    background: linear-gradient(90deg ,#1426CD, #E91E1E);
    transition: 0.5s;
}
.active--s .tabs--wrapper:before {
    opacity: 1;
    width: var(--widthJS2);
    transform: translateX(var(--transform2JS)) translateY(-50%);
}
.tabsItem {
    padding: 3px 20px;
    border-radius: 5px;
    cursor: pointer;
    background: transparent;
    transition: 0.5s;
    opacity: 0;
    /* transform: scale(0.3); */
}

.active--s .tabsItem {
    opacity: 1;
    transform: scale(1);
}

/* .tabsItem:hover {
    background: linear-gradient(90deg ,#1426CD, #E91E1E);
} */
/* .activeTab {
    background: linear-gradient(90deg ,#1426CD, #E91E1E);
} */

@media screen and (max-width: 600px) {

    .tabs--wrapper {
        justify-content: flex-start;
        gap: 0 15px;
        overflow-x: scroll;
        padding: 12px 0;
    }
    .tabs--wrapper::-webkit-scrollbar {
        height: 3px;
    }
    .tabs--wrapper::-webkit-scrollbar-track {
        background: #fff;
    }
    .tabs--wrapper::-webkit-scrollbar-thumb {
        background-color: #1426CD;
        border-radius: unset;
        border: unset;
    }
    .tabsItem {
        font-size: 14px;
        text-wrap: nowrap;
        padding: 3px 15px;
    }
    .tabs--wrapper:before {
        height: 65%;
    }

}

</style>