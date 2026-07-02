<script setup>
import { ref } from 'vue';
import GalleryBtns from './showcaseSection/galleryBtns.vue';
import GalleryImages from './showcaseSection/galleryImages.vue';



const imageGallary = ref([
    {
        imageID: "15",
        imageURL: "shop",
        imageFigmaURL: "https://www.figma.com/design/hlVbD1Q9JzGhYZ3iAA56bg/TakShop?node-id=0-1&t=VL14Ru4KqYriig57-1",
        imageCategory: {
            isMoreThenOneCategoty: false,
            category_1: "web",
        },
        isSpecial: true,
    },
    {
        imageID: "12",
        imageURL: "gaming",
        imageFigmaURL: "https://www.figma.com/design/2wDuQFmBnqDrQWewwwjhM5/Gaming-Website?node-id=0-1&t=ghTs4wfeVRhEVNph-1",
        imageCategory: {
            isMoreThenOneCategoty: false,
            category_1: "web",
        },
    },
    {
        imageID: "11",
        imageURL: "Thumbnail",
        imageFigmaURL: "https://www.figma.com/design/3enOWXqLU3k0JLtxwmt6YC/FitMaster?node-id=0-1&t=U9hHZI1JnclridBI-1",
        imageCategory: {
            isMoreThenOneCategoty: true,
            category_1: "app",
            category_2: "web",
        },
    },
    {
        imageID: "2",
        imageURL: "CinemaCity",
        imageFigmaURL: "https://www.figma.com/file/U2NaEMdeL4Nz0W54Vqm5Us/Midia?type=design&node-id=0%3A1&mode=design&t=7NTbvrlZBagSZyq9-1",
        imageCategory: {
            isMoreThenOneCategoty: true,
            category_1: "app",
            category_2: "web",
        },
    },
    {
        imageID: "6",
        imageURL: "instaGreen",
        imageFigmaURL: "https://www.figma.com/file/ZshausF9yExOGNo4lodN1N/Untitled?type=design&mode=design&t=bdyheiinotnVU75z-1",
        imageCategory: {
            isMoreThenOneCategoty: false,
            category_1: "GraphicDesign",
        },
    },
    {
        imageID: "3",
        imageURL: "Melodies",
        imageFigmaURL: "https://www.figma.com/file/Wj1lFdypYMuj0sDUTDYF6X/melodies-Web?type=design&node-id=0%3A1&mode=design&t=bdyheiinotnVU75z-1",
        imageCategory: {
            isMoreThenOneCategoty: true,
            category_1: "app",
            category_2: "web",
        },
    },
    {
        imageID: "1",
        imageURL: "toureland",
        imageFigmaURL: "https://www.figma.com/design/XFU3GqLTP5b4BKg3JsZRzK/Tour-Website?node-id=0-1&t=wdVEn5syasJmYogd-1",
        imageCategory: {
            isMoreThenOneCategoty: false,
            category_1: "web",
        }
        
    },
    {
        imageID: "4",
        imageURL: "LapKade",
        imageFigmaURL: "https://www.figma.com/design/iDGEQMeJMAAO1zxkgPUce5/Laptop-Byuing-website?node-id=0-1&t=fhTYOL3WC1a1a6k0-1",
        imageCategory: {
            isMoreThenOneCategoty: true,
            category_1: "app",
            category_2: "web",
        },
    },
    {
        imageID: "5",
        imageURL: "asoSoft",
        imageFigmaURL: "https://www.figma.com/file/SxsGiS8mGoIBumxEwBEP2u/Aso-Soft?type=design&mode=design&t=bdyheiinotnVU75z-1",
        imageCategory: {
            isMoreThenOneCategoty: false,
            category_1: "web",
        },
    },
    {
        imageID: "7",
        imageURL: "instaRed",
        imageFigmaURL: "https://www.figma.com/file/Y1yGenm8sOHxRIwHKiquUV/Untitled?type=design&node-id=0%3A1&mode=design&t=hvXBe3rHvU1YDwFj-1",
        imageCategory: {
            isMoreThenOneCategoty: false,
            category_1: "GraphicDesign",
        },
    },
    {
        imageID: "8",
        imageURL: "poster",
        imageFigmaURL: "https://www.figma.com/file/O042Es4gLs6r7eRfDI1ZpY/Untitled?type=design&mode=design&t=wGYwGbEdvDO8moZi-1",
        imageCategory: {
            isMoreThenOneCategoty: false,
            category_1: "GraphicDesign",
        },
    },
    {
        imageID: "9",
        imageURL: "modish",
        imageFigmaURL: "https://www.figma.com/file/E2lCu0Pq4Wjg2Y8dPuyX4B/Modish?type=design&node-id=0-1&mode=design",
        imageCategory: {
            isMoreThenOneCategoty: false,
            category_1: "web",
        },
    },

]);
const filteredImageGallery = ref(imageGallary.value);


function fillterGallery(category) {
    
    if (category === "all") {
        filteredImageGallery.value = imageGallary.value;
    } else {
        filteredImageGallery.value = imageGallary.value.filter (img => { 
            switch (category) {
                case "web":
                    return img.imageCategory.category_1 === "web" || img.imageCategory.category_1 === "app";
                case "app":
                    return img.imageCategory.category_1 === "app";
                case "GraphicDesign":
                    return img.imageCategory.category_1 === "GraphicDesign";
                default:
                    return imageGallary.value;
            }
        })
    }
}

</script>

<template>

    <div class="showcase--wrapper">
        <div class="container">
            <div class="heading--wrapper">
                <h1 class="heading">My Portfolio</h1>
            </div>
       

            <GalleryBtns @filter-gallery="fillterGallery"></GalleryBtns>

            <GalleryImages :filtered-image-gallery="filteredImageGallery"></GalleryImages>

            
        </div> 
    </div>

</template>

<style scoped>



.showcase--wrapper {
    padding: 75px 0;
}

.heading--wrapper {
    text-align: center;
    margin-bottom: 50px;
}

.heading {
    display: inline-block;
    margin: 0 auto;
    color: #fff;
    font-family: bayer;
    border-bottom: 5px solid transparent;
    border-image: linear-gradient(90deg ,#1426CD, #E91E1E) 1;
    letter-spacing: 1px;

    opacity: 0;
    transform: translateY(-35px);
    transition: opacity ease-in-out 1s,
                transform ease-in-out 1s;
}

.active--s .heading {
    opacity: 1;
    transform: translateY(0);
}

.active--s .showcase--wrapper {
    opacity: 1;
    transform: translateY(0);
}
 

</style>