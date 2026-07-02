<script setup>
import { defineProps } from "vue";

const props = defineProps(["filteredImageGallery"]);

</script>

<template>

    <div class="gallery--wrapper">
        <div class="gallery--container">

            <!-- loop -->
                <TransitionGroup name="images">
                    <div class="galleryItem--wrapper activeImg" v-for="img in props.filteredImageGallery" :key="img.imageID" :data-category="img.imageCategory.category_1">

                        <div class="galleryItem" :class="{'galleryItem--hover': img.isSpecial === true}">

                            <div class="imageWrapper">
                                <img class="Gimg" :src="require(`@/assets/projectImages/${img.imageURL}.webp`)">
                                <a :href="img.imageFigmaURL" target="_blank" class="navigateTo--wrapper">
                                    <span class="navigateTxt">discover more in figma</span>
                                    <div class="iconBox">
                                        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
                                            <path stroke-linecap="round" stroke-linejoin="round" d="M13.5 6H5.25A2.25 2.25 0 0 0 3 8.25v10.5A2.25 2.25 0 0 0 5.25 21h10.5A2.25 2.25 0 0 0 18 18.75V10.5m-10.5 6L21 3m0 0h-5.25M21 3v5.25"></path>
                                        </svg>
                                    </div>
                                </a>
                            </div>

                            <div class="galleryItem--tag" v-if="img.isSpecial === true">
                                new
                            </div>

                        </div>

                    </div> 
                </TransitionGroup>
            <!-- loop -->

        </div>
    </div>

</template>

<style scoped>

.gallery--container {
    display: flex;
    justify-content: flex-start;
    position: relative;
    flex-wrap: wrap;
    opacity: 1;
    transition: 0.35s 1s;    
}
.gallery--container::after {
    content: "";
    position: absolute;
    width: 100%;
    height: 100%;
    left: 0;
    top: 0;
    background-color: rgba(56, 56, 56, 0.2);
    border-radius: 15px;
    backdrop-filter: blur(5px);
    opacity: 1;
    transition: 0.5s;
}
.active--s .gallery--container::after {
    opacity: 0;
    height: 0;
}

.galleryItem--wrapper {
    width: 33%;
    max-width: 33%;
    padding: 15px;
    display: flex;
    align-items: center;
    justify-content: center;
    transform-origin: center;
}



.galleryItem {
    width: 100%;
    background: linear-gradient(180deg ,#1426CD, #E91E1E);
    border-radius: 12px;
    transition: 0.35s;
    position: relative;
}

.galleryItem--hover.galleryItem {
    background-size: 200% 200%;
    animation: mbg 2s ease alternate infinite;
}
@keyframes mbg {
    0% {
        background-position: 0% 0%;
    }
    50% {
        background-position: 100% 100%;
    }
    100% {
        background-position: 0% 0%;
    }
}

.galleryItem--tag {
    position: absolute;
    top: 0px;
    left: 24px;
    transform: translateY(-50%);
    padding: 2px 16px;
    background: linear-gradient(to right ,#1426CD, #E91E1E);
    color: #eee;
    font-size: 14px;
    border-radius: 12px;
}

.imageWrapper {
    position: relative;
    width: 100%;
    height: 250px;
    overflow: hidden;
    border-radius: 12px;
    cursor: pointer;
    transform: scale(1);
    transform-origin: center;
    transition: 0.3s;
    display: flex;
    align-items: center;
    justify-content: center;

}
.galleryItem:hover .imageWrapper {
    transform: scale(0.98);
}
.galleryItem--hover .imageWrapper {
    transform: scale(0.98);
}

.Gimg {
    width: 100%;
    height: 100%;
    position: absolute;
    margin-bottom: auto;
    top: 0px;
    left: 0;
    z-index: 0;
    object-fit: cover;
    object-position: left top;
    /* display: none; */
}


.imageWrapper::after {
    content: "";
    position: absolute;
    z-index: 1;
    width: 100%;
    height: 100%;
    /* border-radius: 15px; */
    background-color: rgba(26, 27, 31, 0.5);
    backdrop-filter: blur(5px);

    opacity: 0;
    transition: 0.3s;
}
.galleryItem:hover .imageWrapper::after {
    opacity: 1;
}
.navigateTo--wrapper {
    position: absolute;
    top: 50%;
    left: 50%;
    padding: 8px 12px;
    border-radius: 10px;
    color: #eee;
    font-size: 14px;
    display: inline-flex;
    align-items: center;
    gap: 5px;
    text-transform: capitalize;
    width: auto;
    white-space: nowrap;
    cursor: pointer;
    /* box-shadow: 0 0 15px rgba(238, 238, 238, 0.8); */
    z-index: 2;
    letter-spacing: 0.5px;
    
    
    background-size: 200% auto;
    box-shadow: 0 4px 10px rgba(50, 50, 93, 0.11), 0 1px 3px rgba(0, 0, 0, 0.08);
    background-image: linear-gradient(to right, #1426CD 0%, #E91E1E 50%, #1426CD 100%);
    transform: translate(-50%, -10%);
    opacity: 0;
    transition: 0.5s;

} .navigateTo--wrapper:hover {
    /* background-color: #eee; */
    background-position: right center;
    color: #fff;
    text-shadow: 0 0 5px #000;
} 
.galleryItem:hover .navigateTo--wrapper {
    transform: translate(-50%, -50%);
    opacity: 1;
}

.iconBox {
    width: 25px;
    transform: scale(0.9);
    transition: transform 0.35s;
} .navigateTo--wrapper:hover .iconBox {
    transform: scale(1.1);
}



.images-move, 
.images-leave-active {
  transition: all 0.3s ease;
}
.images-enter-active {
  transition: all 0.5s ease;
}


.images-enter-from,
.images-leave-to {
    transform: scale(0) rotateZ(360deg);
    opacity: 0;
}

.images-leave-active {
  position: absolute;
}


@media screen and (max-width: 991px) {
    .galleryItem--wrapper {
        width: 50%;
        max-width: 50%;
        padding: 12px;
    }
}
@media screen and (max-width: 600px) {
    .galleryItem--wrapper {
        width: 100%;
        max-width: 100%;
        padding: 15px;
    }
    .imageWrapper {
        height: 350px;
    }
    
    .images-enter-from,
    .images-leave-to {
        transform: scale(0);
    }
}

</style>