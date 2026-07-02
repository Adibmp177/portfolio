<script setup>
import { onMounted, ref } from 'vue';


const skillsData = ref([
    {
        id: 2,
        percentageValue: 100,
        progressColor: "#0acf83",
        bgColor: "rgba(48, 36, 40, 0.7)",
        skillClass: "figma",
        skillTitle: "Figma",
        imgURL: "figma",
    },
    {
        id: 4,
        percentageValue: 80,
        progressColor: "#d82885",
        bgColor: "rgba(48, 36, 40, 0.7)",
        skillClass: "AdobeXD",
        skillTitle: "Adobe XD",
        imgURL: "xd",
    },
    {
        id: 1,
        percentageValue: 60,
        progressColor: "#25D4FF",
        bgColor: "rgba(48, 36, 40, 0.7)",
        skillClass: "photoshop",
        skillTitle: "Photoshop",
        imgURL: "ps",
    },
    {
        id: 3,
        percentageValue: 60,
        progressColor: "#ff7919",
        bgColor: "rgba(48, 36, 40, 0.7)",
        skillClass: "illustration",
        skillTitle: "Illustrator",
        imgURL: "al",
    },
]);

onMounted(()=> {

    function startSkills() {
        const circularProgress = document.querySelectorAll(".circular-progress");
        Array.from(circularProgress).forEach((progressBar) => {
            const progressValue = progressBar.querySelector(".percentage");
            const innerCircle = progressBar.querySelector(".inner-circle");
            let startValue = 0,
                endValue = Number(progressBar.getAttribute("data-percentage")),
                speed = 10,
                progressColor = progressBar.getAttribute("data-progress-color");
    
            setTimeout(() => {
                const progress = setInterval(() => {
                    startValue++;
                    progressValue.textContent = `${startValue}%`;
                    progressValue.style.color = `${progressColor}`;
    
                    innerCircle.style.backgroundColor = `${progressBar.getAttribute(
                    "data-inner-circle-color"
                    )}`;
    
                    progressBar.style.background = `conic-gradient(${progressColor} ${
                    startValue * 3.6
                    }deg,${progressBar.getAttribute("data-bg-color")} 0deg)`;
                    if (startValue === endValue) {
                        clearInterval(progress);
                    }
                }, speed);
            }, 1250);
        });
        
    }



    const Observer = new IntersectionObserver((entries)=> {
        entries.forEach(entry => {
            if (entry.isIntersecting) {
                entry.target.classList.add('active');
                Observer.unobserve(entry.target);         
            }
        });
        }, {
            rootMargin: '-45% 0px -30% 0px'
    });
    const Observer_2 = new IntersectionObserver((entries)=> {
        entries.forEach(entry => {
            if (entry.isIntersecting) {
                entry.target.classList.add('active'); 
                startSkills();
                Observer_2.unobserve(entry.target);         
            }
        });
        }, {
            rootMargin: '-45% 0px -30% 0px'
    });

    let aboutItems = document.querySelector('.aboutMeDetails');
    let skillItems = document.querySelector('.skillsWrapper');
    Observer.observe(aboutItems);
    Observer_2.observe(skillItems);

});


</script>

<template>

    <div class="aboutMe--wrapper">
        <div class="container">
            
            <div class="heading--wrapper">
                <h1 class="heading">About me</h1>
            </div>

            <div class="aboutMeContent--wrapper">
                <div class="aboutMeContent">
                    <p class="aboutMe--Txt">
                        Hey there! I'm Adib, your friendly neighborhood <span class="textHighlight">UI/UX designer</span> I’m not just here to make things pretty; I’m all about creating websites and apps <span class="textHighlight">that people love to use</span> And for That I Will make sure that my design is always created based on user needs.
                    </p>
                    <p class="aboutMe--Txt">
                        Riding the wave of the latest <span class="textHighlight">trends</span> is my thing. Your design won’t just be current; it'll be the trendsetter of tomorrow. I will keep an eye on emerging technologies and design movements, ensuring your project doesn't just meet expectations but <span class="textHighlight">surpasses them</span>.
                    </p>
                    <p class="aboutMe--Txt">
                        For me <span class="textHighlight">Your ideas</span> matter most. Let’s team up and make your vision a <span class="textHighlight">digital reality</span>. You can easily contact me through the links that i’ve put in the In the following Part’s.
                    </p>
                </div>
            </div>


            <div class="aboutMeDetails--wrapper">
                <div class="aboutMeDetails">
                    <div class="detailsItem item-1">
                        <span class="Item-description">Location</span>
                        <div class="arrow--warpper">
                            <svg class="svgWidthHeight" viewBox="0 0 181 16" fill="none" xmlns="http://www.w3.org/2000/svg">
                                <path d="M180.707 8.70711C181.098 8.31658 181.098 7.68342 180.707 7.29289L174.343 0.928932C173.953 0.538408 173.319 0.538408 172.929 0.928932C172.538 1.31946 172.538 1.95262 172.929 2.34315L178.586 8L172.929 13.6569C172.538 14.0474 172.538 14.6805 172.929 15.0711C173.319 15.4616 173.953 15.4616 174.343 15.0711L180.707 8.70711ZM0 9H180V7H0V9Z" fill="url(#paint0_linear_19_101)"/>
                                <defs>
                                    <linearGradient id="paint0_linear_19_101" x1="-11.4741" y1="8" x2="195.06" y2="8" gradientUnits="userSpaceOnUse">
                                        <stop stop-color="white"/>
                                        <stop offset="0.0001" stop-color="#1426CD"/>
                                        <stop offset="1" stop-color="#E91E1E"/>
                                        <stop offset="1" stop-color="white"/>
                                    </linearGradient>
                                </defs>
                            </svg>
                        </div>
                        <span class="detail">IRAN</span>
                    </div>
                    <div class="detailsItem item-2">
                        <span class="Item-description">UI/UX Designer Since</span>
                        <div class="arrow--warpper">
                            <svg class="svgWidthHeight" viewBox="0 0 181 16" fill="none" xmlns="http://www.w3.org/2000/svg">
                                <path d="M180.707 8.70711C181.098 8.31658 181.098 7.68342 180.707 7.29289L174.343 0.928932C173.953 0.538408 173.319 0.538408 172.929 0.928932C172.538 1.31946 172.538 1.95262 172.929 2.34315L178.586 8L172.929 13.6569C172.538 14.0474 172.538 14.6805 172.929 15.0711C173.319 15.4616 173.953 15.4616 174.343 15.0711L180.707 8.70711ZM0 9H180V7H0V9Z" fill="url(#paint0_linear_19_101)"/>
                                <defs>
                                    <linearGradient id="paint0_linear_19_101" x1="-11.4741" y1="8" x2="195.06" y2="8" gradientUnits="userSpaceOnUse">
                                        <stop stop-color="white"/>
                                        <stop offset="0.0001" stop-color="#1426CD"/>
                                        <stop offset="1" stop-color="#E91E1E"/>
                                        <stop offset="1" stop-color="white"/>
                                    </linearGradient>
                                </defs>
                            </svg>
                        </div>
                        <span class="detail">2023, July</span>
                    </div>
                    <div class="detailsItem item-3">
                        <span class="Item-description">Working As</span>
                        <div class="arrow--warpper">
                            <svg class="svgWidthHeight" viewBox="0 0 181 16" fill="none" xmlns="http://www.w3.org/2000/svg">
                                <path d="M180.707 8.70711C181.098 8.31658 181.098 7.68342 180.707 7.29289L174.343 0.928932C173.953 0.538408 173.319 0.538408 172.929 0.928932C172.538 1.31946 172.538 1.95262 172.929 2.34315L178.586 8L172.929 13.6569C172.538 14.0474 172.538 14.6805 172.929 15.0711C173.319 15.4616 173.953 15.4616 174.343 15.0711L180.707 8.70711ZM0 9H180V7H0V9Z" fill="url(#paint0_linear_19_101)"/>
                                <defs>
                                    <linearGradient id="paint0_linear_19_101" x1="-11.4741" y1="8" x2="195.06" y2="8" gradientUnits="userSpaceOnUse">
                                        <stop stop-color="white"/>
                                        <stop offset="0.0001" stop-color="#1426CD"/>
                                        <stop offset="1" stop-color="#E91E1E"/>
                                        <stop offset="1" stop-color="white"/>
                                    </linearGradient>
                                </defs>
                            </svg>
                        </div>
                        <span class="detail">Full-time/Part-time Jobs</span>
                    </div>
                </div>
            </div>

            <div class="skillsWrapper">
                <h2 class="skillHeading">My Skills: </h2>
                <div class="skillsContainer">
                    <div class="skills" v-for="skill in skillsData" :key="skill.id" :class="skill.skillClass">
                        <div class="skill">
                            <div class="circular-progress" data-inner-circle-color="transparent" :data-percentage="skill.percentageValue" :data-progress-color="skill.progressColor" :data-bg-color="skill.bgColor">
                                <div class="inner-circle">
                                    <div class="skillIcon">
                                        <img :src="require(`@/assets/skills/${skill.imgURL}.webp`)">
                                    </div>
                                </div>
                                <div class="percentage">0%</div>
                                
                            </div>
                        </div>
                        <p class="skillTitle">{{ skill.skillTitle }}</p>
                    </div>
                </div>
              
            </div>


        </div>

    </div>
   

</template>


<style scoped>

.skillsWrapper {
    margin: 25px 0 50px;
}
.skillsContainer {
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-wrap: wrap;
}
.skillHeading {
    color: #eee;
    margin-bottom: 75px;
    font-size: 24px;
    letter-spacing: 1px;
    font-weight: 500;
    opacity: 0;
    transform: translateX(-15px);
    transition: 0.8s 0.5s;
} .active .skillHeading {
    opacity: 1;
    transform: translateX(0px);
}

.skills {
    width: 25%;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
}

.figma.skills, .illustration.skills {
    transform: translateY(-30px);
    opacity: 0;
    transition: 0.8s 0.7s;
}
.photoshop.skills, .AdobeXD.skills {
    transform: translateY(30px);
    opacity: 0;
    transition: 0.8s 0.7s;
}
.active .photoshop.skills, .active .AdobeXD.skills {
    transform: translateY(0);
    opacity: 1;
}
.active .figma.skills, .active .illustration.skills {
    transform: translateY(0);
    opacity: 1;
}



.circular-progress {
  width: 100px;
  height: 100px;
  /* margin: 100px auto; */
  border-radius: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
  box-shadow: 0 0 15px rgba(238, 238, 238, 0.5);
}
.inner-circle {
  position: absolute;
  width: calc(100px - 10px);
  height: calc(100px - 10px);
  border-radius: 50%;
  overflow: hidden;
}
.inner-circle::after {
    content: "";
    position: absolute;
    left: 0;
    top: -60px;
    width: 100%;
    height: 60px;
    background: rgba(247, 247, 247, 0.2);
    transition: 0.45s;
}
.skills:hover .inner-circle::after {
    top: 100px;
}

.percentage {
  position: absolute;
  font-size: 15px;
  font-weight: 600;
  z-index: 1;
  text-shadow: 0 0 6px #262626;
  bottom: 10px;
  left: 50%;
  transform: translateX(-50%);
  opacity: 0;
  transition: opacity 0.26s 0.7s;
}
.active .percentage {
    opacity: 1;
}
.skillIcon {
    position: absolute;
    width: 100%;
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 5px;
    border-radius: 50%;
    background: #36291e;
    overflow: hidden;
}
.figma .skillIcon {
    background: linear-gradient(135deg, #C99A24 10%, #823EB5 10%, #026640 10%, #005681 80%);

}
.photoshop .skillIcon {
    background: #2d2e4d;
}
.illustration .skillIcon {
    background: #35281b;
}
.AdobeXD .skillIcon {
    background: #592a49;
}

.skillIcon img {
    width: 100%;
}
.figma .skillIcon img {
    transform: scale(1.4) translate(2.5px, -4px)
}
.photoshop .skillIcon img {
    transform: scale(1.1) translate(3px, -2px)
}
.illustration .skillIcon img {
    transform: scale(1.1) translate(2px, -4px)
}
.AdobeXD .skillIcon img {
    transform: scale(1.3) translate(2px, -0px)
}



.svgWidthHeight {
    width: 181px;
    height: 16px;
}
.skillTitle {
    font-size: 16px;
    letter-spacing: 1px;
    font-weight: 600;
    margin-top: 12px;
    text-align: center;
    text-shadow: 0 0 10px rgba(238, 238, 238, 0.5);
}

.figma .skillTitle {
    color: #0acf83;
}
.photoshop .skillTitle {
    color: #25D4FF;
}
.illustration .skillTitle {
    color: #ff7919;
}
.AdobeXD .skillTitle {
    color: #d82885;
}




/* ------------------------------------ */

.aboutMe--wrapper {
    padding: 75px 0;
    /* background: #0000007c; */
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
    transform: translateY(-40px);
    transition: opacity ease-in-out 1s,
                transform ease-in-out 1s;
}
.active--s .heading {
    opacity: 1;
    transform: translateY(0);
}

.aboutMeContent--wrapper {
    margin: 50px 0;
    border-radius: 10px;
    background: linear-gradient(90deg ,#1426CD, #E91E1E);
    padding: 3px;
    border-radius: 15px;
    opacity: 0;
    transform: translateY(40px);
    transition: opacity ease-in-out 1s,
                transform ease-in-out 1s;
    
}
.active--s .aboutMeContent--wrapper {
    opacity: 1;
    transform: translateY(0);
}

.textHighlight {
    color: #eee;
    display: inline-block;
    position: relative;
    font-weight: 600;
}
.textHighlight::after {
    content: "";
    position: absolute;
    width: 0%;
    left: 0;
    bottom: 3px;
    border-bottom: 3px solid transparent;
    border-image: linear-gradient(90deg ,#1426CD, #E91E1E) 1;
    transition: 0.8s 1s;
} .active--s .textHighlight::after {
    width: 100%;
}

.aboutMeContent {
    background-color: rgba(0, 0, 0, 0.8);
    padding: 20px;
    border-radius: 15px;
    color: #fff;
    /* border: 3px solid transparent; */
    /* border-image: linear-gradient(90deg ,#1426CD, #E91E1E) 1; */
    /* border-radius: 10px */
}

.aboutMe--Txt {
    font-size: 18px;
    line-height: 1.57;
    letter-spacing: 0.5px;
}
.aboutMe--Txt:nth-child(2) {
    margin: 12px 0;
}

.detailsItem {
    position: relative;
    display: flex;
    justify-content: space-between;
    align-items: center;
    border-bottom: 1px solid transparent;
    color: #fff;
    border-image: linear-gradient(90deg ,#1426CD, #E91E1E) 1;
}
.detailsItem:not(.detailsItem:last-child) {
    margin-bottom: 20px;
}

.item-1 {
    opacity: 0;
    transform: translateY(15px);
    transition: 0.5s;
}
.item-2 {
    opacity: 0;
    transform: translateY(25px);
    transition: 0.5s 0.3s;
}
.item-3 {
    opacity: 0;
    transform: translateY(30px);
    transition: 0.5s 0.6s;
}
.active .item-1 {
    opacity: 1;
    transform: translateY(0px);
}
.active .item-2 {
    opacity: 1;
    transform: translateY(0px);
}
.active .item-3 {
    opacity: 1;
    transform: translateY(0px);
}


.Item-description {
    font-size: 24px;
}
.detail {
    font-size: 20px;
}

.arrow--warpper {
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
}

@media screen and (max-width:700px) {
    .svgWidthHeight {
        width: 100px;
    }
    .Item-description {
        font-size: 18px;
    }
    .detail {
        font-size: 16px;
    }
    .skills {
        width: 50%;
        padding: 25px 0;
    }   
    .skillHeading {
        font-size: 17px;
        font-weight: 600;
        margin-bottom: 50px;
    }
}

@media screen and (max-width:500px) {
    .svgWidthHeight {
        width: 80px;
        display: none;
    }
    .Item-description {
        font-size: 16px;
    }
    .detail {
        font-size: 14px;
    }
    .CvBtn {
        font-size: 14px !important;
        transform: scale(0.7);
        transform-origin: right;
    }
    .aboutMe--Txt {
        font-size: 16px;
        line-height: 1.8;
    }
}



</style>