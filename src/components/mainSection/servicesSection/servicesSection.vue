<script setup>
import { onMounted, ref } from 'vue';



const serviceItemsData = ref([
    {
        id: 1,
        SVGPaths: [
            {
                path1: "M9 17.25v1.007a3 3 0 0 1-.879 2.122L7.5 21h9l-.621-.621A3 3 0 0 1 15 18.257V17.25m6-12V15a2.25 2.25 0 0 1-2.25 2.25H5.25A2.25 2.25 0 0 1 3 15V5.25m18 0A2.25 2.25 0 0 0 18.75 3H5.25A2.25 2.25 0 0 0 3 5.25m18 0V12a2.25 2.25 0 0 1-2.25 2.25H5.25A2.25 2.25 0 0 1 3 12V5.25",
            }
        ],
        heading: "Web Design",
        description: "In web design, I showcase my passion for creating beautiful and user-friendly interfaces. I pay close attention to intricate details to enhance user experience.",
    },
    {
        id: 2,
        SVGPaths: [
            {
                path1: "M10.5 1.5H8.25A2.25 2.25 0 0 0 6 3.75v16.5a2.25 2.25 0 0 0 2.25 2.25h7.5A2.25 2.25 0 0 0 18 20.25V3.75a2.25 2.25 0 0 0-2.25-2.25H13.5m-3 0V3h3V1.5m-3 0h3m-3 18.75h3",
            }
        ],
        heading: "App Design",
        description: "I love crafting unique user interfaces for mobile applications. My focus lies in ensuring optimal user interaction and attention to detail.",
    },
    {
        id: 3,
        SVGPaths: [
            {
                path1: "M2.25 7.125C2.25 6.504 2.754 6 3.375 6h6c.621 0 1.125.504 1.125 1.125v3.75c0 .621-.504 1.125-1.125 1.125h-6a1.125 1.125 0 0 1-1.125-1.125v-3.75ZM14.25 8.625c0-.621.504-1.125 1.125-1.125h5.25c.621 0 1.125.504 1.125 1.125v8.25c0 .621-.504 1.125-1.125 1.125h-5.25a1.125 1.125 0 0 1-1.125-1.125v-8.25ZM3.75 16.125c0-.621.504-1.125 1.125-1.125h5.25c.621 0 1.125.504 1.125 1.125v2.25c0 .621-.504 1.125-1.125 1.125h-5.25a1.125 1.125 0 0 1-1.125-1.125v-2.25Z",
            }
        ],
        heading: "Responsive Design’s",
        description: "With responsive design, I create layouts that seamlessly adapt to various devices, from smartphones to desktops. My goal is to provide an optimized experience for every user.",
    },
    {
        id: 4,
        SVGPaths: [
            {
                path1: "M12 7.5h1.5m-1.5 3h1.5m-7.5 3h7.5m-7.5 3h7.5m3-9h3.375c.621 0 1.125.504 1.125 1.125V18a2.25 2.25 0 0 1-2.25 2.25M16.5 7.5V18a2.25 2.25 0 0 0 2.25 2.25M16.5 7.5V4.875c0-.621-.504-1.125-1.125-1.125H4.125C3.504 3.75 3 4.254 3 4.875V18a2.25 2.25 0 0 0 2.25 2.25h13.5M6 7.5h3v3H6v-3Z",
            }
        ],
        heading: "Prototype",
        description: "I develop prototypes to simulate user experience and identify improvements. This ensures the final product delivers the best results before launch.",
    },
    {
        id: 5,
        SVGPaths: [
            {
                path1: "M9.53 16.122a3 3 0 0 0-5.78 1.128 2.25 2.25 0 0 1-2.4 2.245 4.5 4.5 0 0 0 8.4-2.245c0-.399-.078-.78-.22-1.128Zm0 0a15.998 15.998 0 0 0 3.388-1.62m-5.043-.025a15.994 15.994 0 0 1 1.622-3.395m3.42 3.42a15.995 15.995 0 0 0 4.764-4.648l3.876-5.814a1.151 1.151 0 0 0-1.597-1.597L14.146 6.32a15.996 15.996 0 0 0-4.649 4.763m3.42 3.42a6.776 6.776 0 0 0-3.42-3.42",
            }
        ],
        heading: "Graphic  Design",
        description: "In graphic design, I use creativity and precision to establish a connection between the user and the brand. My designs convey the brand's identity and message effectively.",
    },
    {
        id: 6,
        SVGPaths: [
            {
                path1: "M9 4.5v15m6-15v15m-10.875 0h15.75c.621 0 1.125-.504 1.125-1.125V5.625c0-.621-.504-1.125-1.125-1.125H4.125C3.504 4.5 3 5.004 3 5.625v12.75c0 .621.504 1.125 1.125 1.125Z",
            }
        ],
        heading: "Wireframe Design",
        description: "Wireframe design involves creating simple and conceptual structures for future projects. This crucial phase in the design process helps to  find optimal solutions for client presentations.",
     },
])

onMounted(()=> {
    const Observer = new IntersectionObserver((entries)=> {
        entries.forEach(entry => {
            if (entry.isIntersecting) {
                entry.target.classList.add('active');
                Observer.unobserve(entry.target);
            }
        });
    }, {
        rootMargin: '-50% 0px -20% 0px'
    });

    let serviceItems = document.querySelectorAll('.servicesItem--container');
    serviceItems.forEach(item => {
        Observer.observe(item);
    });

})

</script>

<template>

    <div class="services--wrapper">
        <div class="container">

            <div class="heading--wrapper">
                <h1 class="heading">My Top Services</h1>
            </div>
            <p class="headingDescription">
                Ready to make your brand <span class="shine">shine</span>? Here's a sneak peek into what I can bring to the table. Take a look at the services below and let's turn your ideas into something awesome:
            </p>


            <div class="servicesItem--wrapper">

                <div class="servicesItem--container" v-for="item in serviceItemsData" :key="item.id">
                    <div class="servicesItem">

                        <div class="icon--wrapper">
                            <div class="icon--caontainer">
                                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6 icon">
                                    <path stroke-linecap="round" stroke-linejoin="round" :d="item.SVGPaths[0].path1" />
                                </svg>
                            </div>
                        </div>

                        <h2 class="serviceHeading">
                            {{ item.heading }}
                        </h2>

                        <p class="serviceDesciption">
                            {{ item.description }}
                        </p>

                    </div>
                </div>
        
            </div>
                        

        </div>
    </div>

</template>


<style scoped>

.services--wrapper {
    padding: 100px 0 75px;
    /* background: radial-gradient(69.9% 149.37% at -7.92% -4.45%, rgba(20, 38, 205, 0.23) 0%, rgba(20, 38, 205, 0.155) 100%), radial-gradient(75.56% 161.46% at -13.58% -6.36%, rgba(233, 30, 30, 0.329) 0%, rgba(233, 30, 30, 0.007) 100%); */
}

.heading--wrapper {
    text-align: center
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
.headingDescription {
    width: 70%;
    font-size: 20px;
    color: #fff;
    text-align: center;
    margin: 30px auto 70px;
    letter-spacing: 0.25px;
    opacity: 0;
    transform: translateY(35px);
    transition: opacity ease-in-out 1s,
                transform ease-in-out 1s;
} .active--s .headingDescription{
    opacity: 1;
    transform: translateY(0);
}
.shine {
    font-family: gagalin;
    color: #FFD700;
    font-weight: 500;
    letter-spacing: 0.9px;
    transition: 0.35s 1.3s;
}
.active--s .shine {
    text-shadow: 0 0 10px #FFD700;
}


.servicesItem--wrapper {
    width: 100%;
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    gap: 40px;
}
.servicesItem--container {
    width: 30%;
    min-height: 100%;
    padding: 2px;
    background: linear-gradient(180deg ,#1426CD, #E91E1E);
    border-radius: 8px;
    box-shadow: 0 0 8px #FFD700;
    cursor: pointer;
    transition: 0.35s;
    transform: scale(0);
    transition: 0.35s;
}
.active.servicesItem--container {
    transition: 1s;
    transform: scale(1);
}


.servicesItem {
    width: 100%;
    height: 100%;
    color: #fff;
    border-radius: 8px;
    background: rgba(0, 0, 0, 0.6);
    backdrop-filter: blur(15px);
    padding: 25px 10px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    text-align: center;
}
.serviceHeading {
    font-size: 22px;
    margin: 10px 0 5px;
    text-shadow: 0 0 10px #000;
}
.serviceDesciption {
    font-size: 14px;
    text-shadow: 0 3px 10px #000;
}
.icon--wrapper {
    width: 82px;
    height: 82px;
    background: linear-gradient(360deg ,#1426CD, #E91E1E);
    background-size: 100% 120%;
    padding: 2px;
    border-radius: 50%;
    /* margin-bottom: auto; */
}
.servicesItem--container:hover {
    transition: 0.35s;
    transform: scale(1.08);
}


.icon--caontainer {
    width: 100%;
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    background: rgba(0, 0, 0, 0.6);
    border-radius: 50%;
}

.icon {
    width: 60%;
    color: #fff;
}


@media screen and (max-width: 991px) {
    .headingDescription {
        width: 100%;
        font-size: 18px;
    }
    .servicesItem--container {
        width: 45%;
    }
    .serviceHeading {
        font-size: 18px;
    }
}

@media screen and (max-width: 500px) {
    .servicesItem--wrapper {
        gap: 40px 0px;
    }
    .headingDescription {
        font-size: 16px;
    }
    .servicesItem--container {
        width: 100%;
    }
    .serviceHeading {
        margin: 10px 0 5px;
        font-size: 16px;
    }
    .serviceDesciption {
        font-size: 12px;
        text-shadow: 0 3px 10px #000;
    }
}


</style>