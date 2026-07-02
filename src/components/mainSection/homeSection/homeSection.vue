<script setup>



</script>

<template>

    <div class="homeWrapper">
        <h1 class="aboutMeTxt">
            HI, I AM <br> 
            <span class="myName">Adib Mohammad Pouri</span>
        </h1>
        <p class="intro">
            I’m a <span>UI/UX Designer</span> and i will be glad to share my work with you. Jump into a world where modern design works for your business. I design websites that not only look great but also bring in more clients and help your sales grow.
        </p>
        <div class="homeButton--wrapper">
            <button class="home-btns contactMe--btn"><a href="#contact">Contact Me</a></button>
            <button class="home-btns myPortfolio--btn"><a href="#Portfolio">My Portfolio</a></button>
        </div>
    </div>
    <a href="#aboutMe" class="scrollDown">
        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6">
            <path stroke-linecap="round" stroke-linejoin="round" d="m4.5 5.25 7.5 7.5 7.5-7.5m-15 6 7.5 7.5 7.5-7.5" />
        </svg>
    </a>

</template>

<style scoped>
.scrollDown {
    display: inline-block;
    position: absolute;
    bottom: 25px;
    left: 50%;
    transform: translate(-50%, 0);
    width: 45px;
    padding: 5px;
    color: #eee;
    animation: moving 0.8s alternate infinite linear;
    opacity: 0;
    transition: opacity 0.5s 1s;
}
.active--s .scrollDown {
    opacity: 1;
}
@keyframes moving {
    0% {
        transform: translate(-50%, 0px);
    }
    100% {
        transform: translate(-50%, -15px);
    }
}

.homeWrapper {
    text-align: center;
    color: var(--main-txt);
    padding-top: 50px;
}

.aboutMeTxt {
    font-size: 40px;
    font-family: gagalin; 
    opacity: 0;
    transform: translateY(25px);
    letter-spacing: 1px;
    margin-bottom: 30px;
    text-shadow: 0 0 5px #000;
    transition: opacity 1s 0.2s ease-in-out,
                transform 1s 0.2s ease-in-out;
}
.myName {
    display: block;
    font-family: gagalin;
    background-image: linear-gradient(90deg ,#1426CD 30%, #E91E1E 65%);
    background-clip: text;
    -webkit-background-clip: text;
    color: transparent;
    text-shadow: none;
}

.intro {
    font-size: 20px;
    margin: 40px 0 35px;
    line-height: 1.65;
    font-weight: 500;
    letter-spacing: 0.5px;
    font-family: vazir;
    color: #fff;
    padding: 0 250px;

    opacity: 0;
    transform: translateY(40px);
    transition: opacity 1s 0.4s ease-in-out,
                transform 1s 0.4s ease-in-out;
}

.active--s .intro {
    opacity: 0.7;
    transform: translateY(0px);
} 



.homeButton--wrapper {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 0 15px;
}
.home-btns {
    background-color: unset;
    border: none;
    transform: translateY(50px);
    transition: opacity 1s 0.6s ease-in-out,
    transform 1s 0.6s ease-in-out,
    background-color 0.35s;
}
.contactMe--btn {
    opacity: 0;
}
.contactMe--btn a, .myPortfolio--btn a {
    font-size: 20px;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 6px 48px;
    border-radius: 5px;
    color: #fff;
    cursor: pointer;
    letter-spacing: 1.1px;
}

.contactMe--btn a{
    background-size: 200% auto;
    background-image: linear-gradient(to right, #1426CD 0%, #E91E1E 50%, #1426CD 100%);
    transition: 0.35s;
    transform: scale(1.02);
} .contactMe--btn a:hover{
    background-position: right center;
}


.myPortfolio--btn {
    opacity: 0;
    padding: 2px;
    border-radius: 5px;
    background-size: 200% auto;
    background-image: linear-gradient(to left, #1426CD 0%, #E91E1E 50%, #1426CD 100%);
    transition: background-position 0.45s,
                opacity 1s 0.6s ease-in-out,
                transform 1s 0.6s ease-in-out;
}
.myPortfolio--btn a {
    background: rgba(0, 0, 0, 0.8);
    border-radius: 5px;
    transition: background 0.2s;
    /* transition: 0.5s; */
} .myPortfolio--btn:hover{
    background-position: right center;
}
.myPortfolio--btn:hover a {
    background: rgba(0, 0, 0, 0.5);
}

.active--s .aboutMeTxt,
.active--s .contactMe--btn, .active--s .myPortfolio--btn {
    opacity: 1;
    transform: translateY(0px);
}

@media screen and (max-width: 991px) {
    .intro {
        padding: 0 50px;
    }
}

@media screen and (max-width: 768px) {
    .homeWrapper {
        padding: 50px 0;
    }
    .aboutMeTxt {
        font-size: 32px;
    }
    .intro {
        padding: 0 35px;
    }

    .contactMe--btn a, .myPortfolio--btn a {
        padding: 7px 32px;
        font-size: 17px;
    }
}

@media screen and (max-width: 450px) {
    .aboutMeTxt {
        font-size: 26px;
    }
    .intro {
        padding: 0 20px;
        font-size: 16px;
    }
    .homeButton--wrapper {
        flex-direction: column;
        gap: 15px 0;
    }
    .myPortfolio--btn {
        order: 0;
    }
    .contactMe--btn {
        order: 0;
    }
}

</style>