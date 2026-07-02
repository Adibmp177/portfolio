<script setup>
import { ref } from 'vue';


function addErrorClass(input) {
    input.nextElementSibling.classList.remove('yesError');
    input.classList.remove('invalid'); 
    input.classList.add('valid');
}
function removeErrorCalss(input) {
    input.nextElementSibling.classList.add('yesError');
    input.classList.remove('valid');
    input.classList.add('invalid');
}
function resetForm() {
    getUserName.value = '';
    getUserEmail.value = '';
    getUsersMessage.value = '';
    isEmailValidat.value = false;
    isNameValidat.value = false;
    isMessageValidat.value = false;
    
    document.querySelector('#txt').classList.remove('valid');
    document.querySelectorAll('.input').forEach((x)=> {
        x.classList.remove('valid');
    });
    document.querySelectorAll('.inputError').forEach((x)=> {
        x.classList.remove('yesError')
    });
}

const getUserName = ref('');
const getUsersMessage = ref('');
const getUserEmail = ref('');

const isNameValidat = ref(false);
const isEmailValidat = ref(false);
const isMessageValidat = ref(false);

const regEx_name = /^[a-zA-Z]+$/;
const regEx_email = /^[a-zA-Z0-9.!#$%&'*+/=?^_`{|}~-]+@[a-zA-Z0-9](?:[a-zA-Z0-9-]{0,61}[a-zA-Z0-9])?(?:\.[a-zA-Z0-9](?:[a-zA-Z0-9-]{0,61}[a-zA-Z0-9])?)*$/

function validateName(input) {
    const inputLength = input.value.length >= 3;
    if (regEx_name.test(getUserName.value) && inputLength) {
        isNameValidat.value = true;
        addErrorClass(input);
    } else {
        isNameValidat.value = false;
        removeErrorCalss(input);
    }
}
function validateEmail(input) {
    if (regEx_email.test(getUserEmail.value)) {
        isEmailValidat.value = true;
        addErrorClass(input);
    } else {
        isEmailValidat.value = false;
        removeErrorCalss(input);
    }
}
function validateMessage(input) {
    if (input.value.length >= 15) {
        isMessageValidat.value = true;
        addErrorClass(input);
    } else {
        isMessageValidat.value = false;
        removeErrorCalss(input);
    }
}


const formLoading = ref(false);
const isSuccessful = ref(false);
const isError = ref(false);

async function sendEmail(e) {
    console.log('wow');
    e.preventDefault();
    if (isNameValidat.value && isEmailValidat.value && isMessageValidat.value) {
        formLoading.value = true;
        let data = new FormData(e.target);
        fetch(e.target.action, {
            method: e.target.method,
            body: data,
            headers: {
                'Accept': 'application/json'
            }
        }).then(response => {
            if (response.ok) {
                formLoading.value = false;
                isSuccessful.value = true;
                setTimeout(() => {
                    isSuccessful.value = false;
                }, 2500);
                e.target.reset();
                resetForm();
            } else {
                formLoading.value = false;
                alert('please try again');
            }
        }).catch(() => {
            alert('please try again');
            formLoading.value = false;
        });
    } else {
        isError.value = true;
        setTimeout(() => {
            isError.value = false;
        }, 2500);
    }
}






</script>

<template>

    <div class="contactSection---wrapper">
        <div class="container">
            <div class="heading--wrapper">
                <h1 class="heading">Contact Me</h1>
            </div>
            <p class="explain">
                In This Part You Can Easily Send Me Any Kind Of Massage Or Offers And I'll Be Happy To Resive Them And Answer Them In Soce Case's.
            </p>
    
            
            <div class="contactMeSection--wrapper">
                
                <div class="contactMeSection">
                    
                    <div class="formWrapper">
                        <form class="form" action="https://formspree.io/f/xgegyvjp" method="post" @submit="sendEmail($event)">
            
                            <div class="inputs---wrapper">
                                <div class="inputGroup">
                                    <input type="text" name="name" id="name" class="input" placeholder="Enter Your Name Here ..." autocomplete="off" v-model="getUserName" @focusout="validateName($event.currentTarget)">
                                    <div class="inputError">
                                        <div class="errorTxt errorTxt-1">
                                            <div class="circle"></div>
                                            Enter text only, not numbers
                                        </div>
                                        <div class="errorTxt errorTxt-2">
                                            <div class="circle"></div>
                                            At least 3 characters
                                        </div>
                                    </div>
                                </div>
                                <div class="inputGroup">
                                    <input type="email" name="email" id="email" class="input" placeholder="Enter Your Email Here ..." autocomplete="off" v-model="getUserEmail" @focusout="validateEmail($event.currentTarget)">
                                
                                    <div class="inputError">
                                        <div class="errorTxt errorTxt-1">
                                            <div class="circle"></div>
                                            Enter the correct email structure: example@gmail.com
                                        </div>
                                    </div>
            
                                </div>
                            </div>
            
                            <div class="inputGroup">
                                <textarea name="message" id="txt" cols="100%" rows="7" placeholder="Your Massage ..." autocomplete="off" v-model="getUsersMessage" @focusout="validateMessage($event.currentTarget)"></textarea>
                                <div class="inputError">
                                    <div class="errorTxt errorTxt-1">
                                        <div class="circle"></div>
                                        Please enter at least 15 characters
                                    </div>
                                </div>
                            </div>
            
                            <input type="submit" value="Send" class="btn">
            
                        </form>
                        <div class="formLoading" v-if="formLoading">
                            <span class="loader"></span>
                        </div>
                        <Transition>
                            <div class="formPopUp formPopUp--ok" v-if="isSuccessful">
                                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6 popIcon">
                                    <path stroke-linecap="round" stroke-linejoin="round" d="M9 12.75 11.25 15 15 9.75M21 12a9 9 0 1 1-18 0 9 9 0 0 1 18 0Z" />
                                </svg>
                                <p class="popUoTxt">Your email has been sent successfully</p>
                            </div>
                        </Transition>
                        <Transition>
                            <div class="formPopUp formPopUp--error" v-if="isError">
                                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6 popIcon">
                                    <path stroke-linecap="round" stroke-linejoin="round" d="m9.75 9.75 4.5 4.5m0-4.5-4.5 4.5M21 12a9 9 0 1 1-18 0 9 9 0 0 1 18 0Z" />
                                </svg>
                                <p class="popUoTxt">Invalid Data</p>
                            </div>
                        </Transition>
                    </div>

                    <div class="contactInfoWrapper">

                        <div class="contactInfo">

                            <div class="contactInfoItem">
                                <div class="contactInfoIconBox">
                                    <div class="contactInfoIcon">
                                        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6 icon">
                                            <path stroke-linecap="round" stroke-linejoin="round" d="M21.75 6.75v10.5a2.25 2.25 0 0 1-2.25 2.25h-15a2.25 2.25 0 0 1-2.25-2.25V6.75m19.5 0A2.25 2.25 0 0 0 19.5 4.5h-15a2.25 2.25 0 0 0-2.25 2.25m19.5 0v.243a2.25 2.25 0 0 1-1.07 1.916l-7.5 4.615a2.25 2.25 0 0 1-2.36 0L3.32 8.91a2.25 2.25 0 0 1-1.07-1.916V6.75" />
                                        </svg>
                                    </div>
                                </div>
                                <div class="mainContactInfo">
                                    <div class="contactInfoHeading">Gmail</div>
                                    <div class="mb main"> 
                                        Mohammadpouriadib@gmail.com
                                        <span class="mbDetails">(Main)</span>
                                    </div>
                                    <div class="mb backup"> 
                                        Mohammadppouriadib@gmail.com
                                        <span class="mbDetails">(Backup)</span>
                                    </div>
                                </div>
                            </div>

                            <div class="contactInfoItem">
                                <div class="contactInfoIconBox">
                                    <div class="contactInfoIcon">
                                        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6 icon">
                                            <path stroke-linecap="round" stroke-linejoin="round" d="M2.25 6.75c0 8.284 6.716 15 15 15h2.25a2.25 2.25 0 0 0 2.25-2.25v-1.372c0-.516-.351-.966-.852-1.091l-4.423-1.106c-.44-.11-.902.055-1.173.417l-.97 1.293c-.282.376-.769.542-1.21.38a12.035 12.035 0 0 1-7.143-7.143c-.162-.441.004-.928.38-1.21l1.293-.97c.363-.271.527-.734.417-1.173L6.963 3.102a1.125 1.125 0 0 0-1.091-.852H4.5A2.25 2.25 0 0 0 2.25 4.5v2.25Z" />
                                        </svg>
                                    </div>
                                </div>
                                <div class="mainContactInfo">
                                    <div class="contactInfoHeading">Phone Number</div>
                                    <div class="mb main"> 
                                        +989399866466
                                        <span class="mbDetails">(Main)</span>
                                    </div>
                                    <div class="mb backup"> 
                                        +989337887112
                                        <span class="mbDetails">(Backup)</span>
                                    </div>
                                </div>
                            </div>

                            <div class="contactInfoItem">
                                <div class="contactInfoIconBox">
                                    <div class="contactInfoIcon">
                                        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6 icon">
                                            <path stroke-linecap="round" stroke-linejoin="round" d="M15 10.5a3 3 0 1 1-6 0 3 3 0 0 1 6 0Z" />
                                           <path stroke-linecap="round" stroke-linejoin="round" d="M19.5 10.5c0 7.142-7.5 11.25-7.5 11.25S4.5 17.642 4.5 10.5a7.5 7.5 0 1 1 15 0Z" />
                                        </svg>
                                    </div>
                                </div>
                                <div class="mainContactInfo">
                                    <div class="contactInfoHeading">Location</div>
                                    <div class="mb Main"> 
                                        IRAN
                                    </div>
                                    <div class="mb Backup"> 
                                        Azerbaijan gharbi, Sardash
                                    </div>
                                </div>
                            </div>

                            <div class="socialMediaWrapper">
                                <div class="socailMedaiHeading">
                                    Visit My social Profile And Get Connected:
                                </div>
                                <div class="socialmeidas">
                                    <a href="https://www.linkedin.com/in/adibmohammadpouri/" target="_blank" aria-label="my linkedin Icon" class="socialBox">
                                        <svg xmlns="http://www.w3.org/2000/svg" x="0px" y="0px" width="100" height="100" viewBox="0 0 26 26" class="socialIcon">
                                            <path d="M 21.125 0 L 4.875 0 C 2.183594 0 0 2.183594 0 4.875 L 0 21.125 C 0 23.816406 2.183594 26 4.875 26 L 21.125 26 C 23.816406 26 26 23.816406 26 21.125 L 26 4.875 C 26 2.183594 23.816406 0 21.125 0 Z M 8.039063 22.070313 L 4 22.070313 L 3.976563 9.976563 L 8.015625 9.976563 Z M 5.917969 8.394531 L 5.894531 8.394531 C 4.574219 8.394531 3.722656 7.484375 3.722656 6.351563 C 3.722656 5.191406 4.601563 4.3125 5.945313 4.3125 C 7.289063 4.3125 8.113281 5.191406 8.140625 6.351563 C 8.140625 7.484375 7.285156 8.394531 5.917969 8.394531 Z M 22.042969 22.070313 L 17.96875 22.070313 L 17.96875 15.5 C 17.96875 13.910156 17.546875 12.828125 16.125 12.828125 C 15.039063 12.828125 14.453125 13.558594 14.171875 14.265625 C 14.066406 14.519531 14.039063 14.867188 14.039063 15.222656 L 14.039063 22.070313 L 9.945313 22.070313 L 9.921875 9.976563 L 14.015625 9.976563 L 14.039063 11.683594 C 14.5625 10.875 15.433594 9.730469 17.519531 9.730469 C 20.105469 9.730469 22.039063 11.417969 22.039063 15.046875 L 22.039063 22.070313 Z"></path>
                                        </svg>
                                    </a>  
                                    <a href="https://dribbble.com/adibmohammadpouri" target="_blank" aria-label="my dribbble Icon" class="socialBox">
                                        <svg xmlns="http://www.w3.org/2000/svg" x="0px" y="0px" width="100" height="100" viewBox="0 0 48 48" class="socialIcon">
                                            <path d="M 24 4 C 12.972066 4 4 12.972074 4 24 C 4 35.027926 12.972066 44 24 44 C 35.027934 44 44 35.027926 44 24 C 44 12.972074 35.027934 4 24 4 z M 24 7 C 28.142307 7 31.929518 8.4763377 34.875 10.927734 C 32.122374 13.351092 28.974768 15.323142 25.580078 16.835938 C 23.811529 13.61959 21.891654 10.500767 19.736328 7.5585938 C 21.100562 7.2070927 22.524179 7 24 7 z M 16.785156 8.6171875 C 18.997535 11.542724 20.949628 14.664262 22.746094 17.886719 C 19.050465 19.170625 15.137713 20 11 20 C 9.8323552 20 8.6813446 19.922155 7.5390625 19.810547 C 8.7969115 14.835264 12.230939 10.75149 16.785156 8.6171875 z M 37.001953 13.046875 C 39.461176 15.964926 40.9535 19.721786 40.992188 23.837891 C 38.832662 23.296195 36.575941 23 34.25 23 C 32.4219 23 30.655764 23.235969 28.925781 23.574219 C 28.323231 22.178362 27.663283 20.821807 26.984375 19.46875 C 30.643681 17.813906 34.040456 15.676234 37.001953 13.046875 z M 24.177734 20.570312 C 24.811258 21.821635 25.45011 23.063845 26.015625 24.353516 C 19.953229 26.24965 14.749259 30.09875 11.257812 35.238281 C 8.6153572 32.243192 7 28.319322 7 24 C 7 23.585614 7.0335222 23.180292 7.0625 22.773438 C 8.3577913 22.906235 9.665848 23 11 23 C 15.643379 23 20.045102 22.063249 24.177734 20.570312 z M 34.25 26 C 36.498791 26 38.668342 26.319367 40.738281 26.882812 C 39.953494 31.489342 37.336086 35.457573 33.644531 38.001953 C 32.755328 34.064901 31.510607 30.269114 30.085938 26.5625 C 31.460152 26.325929 32.807024 26 34.25 26 z M 27.091797 27.125 C 28.662683 31.125628 30.006215 35.241408 30.90625 39.53125 C 28.795754 40.468547 26.462824 41 24 41 C 20.010678 41 16.357113 39.622608 13.460938 37.332031 C 16.608874 32.477365 21.430763 28.841138 27.091797 27.125 z"></path>
                                        </svg>
                                    </a>       
                                    <a href="https://t.me/Adibmohamadpori" target="_blank" aria-label="my telegram Icon" class="socialBox">
                                        <svg xmlns="http://www.w3.org/2000/svg" x="0px" y="0px" width="100" height="100" viewBox="0 0 32 32" class="socialIcon">
                                            <path d="M 26.070313 3.996094 C 25.734375 4.011719 25.417969 4.109375 25.136719 4.21875 L 25.132813 4.21875 C 24.847656 4.332031 23.492188 4.902344 21.433594 5.765625 C 19.375 6.632813 16.703125 7.757813 14.050781 8.875 C 8.753906 11.105469 3.546875 13.300781 3.546875 13.300781 L 3.609375 13.277344 C 3.609375 13.277344 3.25 13.394531 2.875 13.652344 C 2.683594 13.777344 2.472656 13.949219 2.289063 14.21875 C 2.105469 14.488281 1.957031 14.902344 2.011719 15.328125 C 2.101563 16.050781 2.570313 16.484375 2.90625 16.722656 C 3.246094 16.964844 3.570313 17.078125 3.570313 17.078125 L 3.578125 17.078125 L 8.460938 18.722656 C 8.679688 19.425781 9.949219 23.597656 10.253906 24.558594 C 10.433594 25.132813 10.609375 25.492188 10.828125 25.765625 C 10.933594 25.90625 11.058594 26.023438 11.207031 26.117188 C 11.265625 26.152344 11.328125 26.179688 11.390625 26.203125 C 11.410156 26.214844 11.429688 26.21875 11.453125 26.222656 L 11.402344 26.210938 C 11.417969 26.214844 11.429688 26.226563 11.441406 26.230469 C 11.480469 26.242188 11.507813 26.246094 11.558594 26.253906 C 12.332031 26.488281 12.953125 26.007813 12.953125 26.007813 L 12.988281 25.980469 L 15.871094 23.355469 L 20.703125 27.0625 L 20.8125 27.109375 C 21.820313 27.550781 22.839844 27.304688 23.378906 26.871094 C 23.921875 26.433594 24.132813 25.875 24.132813 25.875 L 24.167969 25.785156 L 27.902344 6.65625 C 28.007813 6.183594 28.035156 5.742188 27.917969 5.3125 C 27.800781 4.882813 27.5 4.480469 27.136719 4.265625 C 26.769531 4.046875 26.40625 3.980469 26.070313 3.996094 Z M 25.96875 6.046875 C 25.964844 6.109375 25.976563 6.101563 25.949219 6.222656 L 25.949219 6.234375 L 22.25 25.164063 C 22.234375 25.191406 22.207031 25.25 22.132813 25.308594 C 22.054688 25.371094 21.992188 25.410156 21.667969 25.28125 L 15.757813 20.75 L 12.1875 24.003906 L 12.9375 19.214844 C 12.9375 19.214844 22.195313 10.585938 22.59375 10.214844 C 22.992188 9.84375 22.859375 9.765625 22.859375 9.765625 C 22.886719 9.3125 22.257813 9.632813 22.257813 9.632813 L 10.082031 17.175781 L 10.078125 17.15625 L 4.242188 15.191406 L 4.242188 15.1875 C 4.238281 15.1875 4.230469 15.183594 4.226563 15.183594 C 4.230469 15.183594 4.257813 15.171875 4.257813 15.171875 L 4.289063 15.15625 L 4.320313 15.144531 C 4.320313 15.144531 9.53125 12.949219 14.828125 10.71875 C 17.480469 9.601563 20.152344 8.476563 22.207031 7.609375 C 24.261719 6.746094 25.78125 6.113281 25.867188 6.078125 C 25.949219 6.046875 25.910156 6.046875 25.96875 6.046875 Z"></path>
                                        </svg>
                                    </a>   
                                    <a href="https://www.behance.net/adibmohammadpouri" target="_blank" aria-label="my behance Icon" class="socialBox">
                                        <svg xmlns="http://www.w3.org/2000/svg" x="0px" y="0px" width="100" height="100" viewBox="0 0 32 32" class="socialIcon">
                                            <path d="M 1 6.75 L 1 25.25 L 9.9375 25.25 C 10.765625 25.25 16.46875 25.082031 16.46875 19.875 C 16.46875 16.621094 14.230469 15.515625 13.09375 15.1875 C 13.929688 14.792969 15.59375 13.855469 15.59375 11.34375 C 15.59375 9.945313 15.394531 6.75 9.6875 6.75 Z M 21.375 8.46875 L 21.375 10.15625 L 28.28125 10.15625 L 28.28125 8.46875 Z M 5.0625 9.90625 L 8.875 9.90625 C 9.234375 9.90625 11.65625 9.714844 11.65625 12.03125 C 11.65625 14.011719 9.90625 14.21875 9.1875 14.21875 L 5.0625 14.21875 Z M 25 11.6875 C 19.777344 11.6875 18.6875 16.222656 18.6875 18.1875 C 18.6875 24.019531 23.46875 24.6875 25 24.6875 C 29.128906 24.6875 30.300781 22.015625 30.78125 20.53125 L 27.78125 20.53125 C 27.664063 20.914063 26.789063 22.15625 25.125 22.15625 C 22.335938 22.15625 22.09375 19.976563 22.09375 19 L 30.96875 19 C 31.148438 15.625 29.671875 11.6875 25 11.6875 Z M 24.90625 14.21875 C 25.738281 14.21875 26.410156 14.460938 26.8125 14.90625 C 27.214844 15.355469 27.511719 16.011719 27.59375 16.875 L 22.09375 16.875 C 22.109375 16.636719 22.164063 16.363281 22.25 16.0625 C 22.335938 15.753906 22.46875 15.460938 22.6875 15.1875 C 22.90625 14.917969 23.210938 14.683594 23.5625 14.5 C 23.921875 14.3125 24.367188 14.21875 24.90625 14.21875 Z M 5.0625 17 L 9.46875 17 C 10.34375 17 12.40625 17.136719 12.40625 19.65625 C 12.40625 22.097656 9.808594 22.09375 9.40625 22.09375 L 5.0625 22.09375 Z"></path>
                                        </svg>
                                    </a>  
                                </div>
                            </div>

                        </div>

                    </div>

                </div>

            </div>

        </div>

    </div>

</template>

<style scoped>


.contactMeSection {
    display: flex;
    align-items: center;
}
.contactInfoWrapper {
    width: 50%;
    padding: 15px 10px;
    height: 100%;
}
.contactInfo {
    height: 100%;
    display: flex;
    flex-direction: column;
    gap: 30px 0;
}
.contactInfoItem {
    display: flex;
    align-items: center;
    opacity: 0;
    transform: translateX(-25px);
    transition: 0.5s 0.8s;
} 
.socialMediaWrapper {
    opacity: 0;
    transform: translateX(-25px);
    transition: 0.5s 0.8s;
}
.active--s .contactInfoItem, .active--s .socialMediaWrapper{
    opacity: 1;
    transform: translateX(0);
}
.contactInfoIconBox {
    width: 60px;
    height: 60px;
    color: #fff;
    background: linear-gradient(45deg ,#1426CD, #E91E1E);
    padding: 2px;
    border-radius: 5px;
}
.contactInfoIcon {
    width: 100%;
    height: 100%;
    background: #000;
    border-radius: 5px;
    display: flex;
    align-items: center;
    justify-content: center;
}
.icon {
    width: 60%;
}
.mainContactInfo {
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    padding-left: 12px;
}
.contactInfoHeading {
    color: #fff;
    font-size: 16px;
    font-weight: 600;
}
.mb {
    font-size: 14px;
    color: #fff;
    font-weight: 500;
}
.main .mbDetails {
    color: #E91E1E;
    font-weight: 600;
}
.backup .mbDetails {
    color: #1426CD;
    font-weight: 600;
}
.mbDetails {
    padding-left: 4px;
}

.socailMedaiHeading {
    font-weight: 600;
    margin-bottom: 8px;
    color: #fff;
}
.socialmeidas {
    display: flex;
    align-items: center;
    gap: 30px;
}
.socialWrapper {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 40px;
}
.socialBox {
    width: 35px;
    height: 35px;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    color: #eee;
    transition: 0.35s;
}

.socialBox:hover {
    transform: scale(1.1);
}
.socialIcon{
    fill: #eee;
}

/** Heading */
.heading--wrapper {
    text-align: center;
    margin-bottom: 35px;
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
    transform: translateY(-50px);
    transition: opacity ease-in-out 1s,
                transform ease-in-out 1s;
}

.active--s .heading {
    opacity: 1;
    transform: translateY(0);
}
.explain {
    line-height: 1.45;
    width: 70%;
    font-size: 16px;
    color: var(--main-txt);
    text-align: center;
    margin: 0 auto 50px;

    opacity: 0;
    transform: translateY(45px);
    transition: 0.5s ease-in-out 0.3s; 
} .active--s .explain {
    opacity: 0.9;
    transform: translateY(0);
}
/** Heading */


.v-enter-active,
.v-leave-active {
  transition: opacity 0.3s ease;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}

.formPopUp {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    padding: 8px 15px;
    color: #fff;
    border-radius: 10px;
    display: flex;
    flex-direction: column;
    align-items: center;
    border-bottom: 3px solid rgb(80, 80, 80);
    text-align: center;
    box-shadow: 0 0 15px #2b2b2b;
}
.formPopUp--ok {
    background-color: #60d394;
}

.formPopUp--error {
    background-color: #ee6055;
}
.popIcon {
    width: 50px;
    height: 50px;
    margin-bottom: 10px;
}
.loader {
  width: 8px;
  height: 40px;
  border-radius: 4px;
  display: block;
  margin: 20px auto;
  position: relative;
  background: currentColor;
  color: #0082f3;
  box-sizing: border-box;
  animation: animloader 0.3s 0.3s linear infinite alternate;
}

.loader::after, .loader::before {
  content: '';
  width: 8px;
  height: 40px;
  border-radius: 4px;
  background: currentColor;
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  left: 20px;
  box-sizing: border-box;
  animation: animloader 0.3s  0.45s  linear infinite alternate;
}
.loader::before {
  left: -20px;
  animation-delay: 0s;
}
@keyframes animloader {
  0%   { height: 48px} 
  100% { height: 4px}
}
.inputError {
    padding-left: 15px;
    color: rgb(233, 57, 57);
    letter-spacing: 0.5px;
    font-size: 14px;
    display: none;
    flex-direction: column;
    gap: 5px;
}
.circle {
    width: 5px;
    height: 5px;
    border-radius: 50%;
    background-color: rgb(206, 19, 19);
    margin-right: 7px;
}
.errorTxt {
    display: flex;
    align-items: center;
}
.yesError {
    display: flex;
}

.contactSection---wrapper {
    padding: 100px 0 75px;
    /* background: radial-gradient(69.9% 149.37% at -7.92% -4.45%, rgba(20, 38, 205, 0.23) 0%, rgba(20, 38, 205, 0.155) 100%), radial-gradient(75.56% 161.46% at -13.58% -6.36%, rgba(233, 30, 30, 0.329) 0%, rgba(233, 30, 30, 0.007) 100%); */

}

.formWrapper {
    width: 50%;
    position: relative;
    opacity: 0;
    padding: 15px 0px;
    transform: translateY(65px);
    transition: 0.7s ease-in-out 0.8s; 
} .active--s .formWrapper {
    opacity: 1;
    transform: translateY(0px);
}

.formLoading {
    width: 100%;
    height: 100%;
    top: 0;
    left: 0;
    border-radius: 15px;
    position: absolute;
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: #eeeeee1a;
    backdrop-filter: blur(7px);
}


.form {
    width: 85%;
    margin: 0 auto;
}

 



.inputs---wrapper {
    display: flex;
    flex-direction: column;
    /* align-items: flex-start; */
    gap: 20px;
    margin-bottom: 30px;
}
.inputGroup {
    display: flex;
    flex-direction: column;
    width: 100%;
    gap: 7px;
} .inputGroup label {
    font-size: 14px;
    color: var(--main-txt);
    font-weight: 600;
    text-transform: capitalize;
}
.input {
    padding: 8px 12px;
    font-size: 14px; 
    color: var(--main-txt);
    outline: none;
    background-color: #fff;
    border: 2px solid #fff;
    border-radius: 5px;
    transition: 0.35s;
    color: #333;
    font-weight: 600;
} .input::placeholder {
    font-weight: 500;
}
.input:focus {
    border-color: var(--third-bg);
}
.valid {
    border-color:rgb(65, 199, 65);
}
.invalid {
    border-color: rgb(206, 19, 19);
}

textarea {
    padding: 8px 12px;
    font-size: 15px; 
    color: var(--main-txt);
    outline: none;
    background-color: #fff;
    border: 2px solid #fff;
    border-radius: 5px;
    transition: 0.35s;
    resize: none;
    color: #333;
    font-weight: 600;
}
textarea:focus {
    border-color: var(--third-bg);
} textarea::placeholder {
    font-weight: 500;
}

.btn {
    display: block;
    padding: 8px;
    color: #eee;
    font-size: 18px;
    font-weight: 600;
    border-radius: 8px;
    background-size: 200% auto;
    background-image: linear-gradient(to right, #E91E1E 0%, #1426CD 50%, #E91E1E 100%);
    width: 100%;
    transition: 0.35s;
    text-shadow: 0 0 5px #000;
    cursor: pointer;
    margin-top: 10px;
    border: none;
    outline: none;
}
.btn:hover {
    background-position: right center;
    transform: scale(1.05, 1.095)
}

@media screen and (max-width:768px) {
    .explain {
        font-size: 14px;
        font-weight: 500;
        width: 100%;
    }
    .contactMeSection {
        flex-direction: column;
        align-items: unset;
    }
    .contactInfoWrapper {
        width: 100%;
        height: auto;
        padding: 40px 0 25px;
    }   
    .formWrapper {
        width: 100%;
    }   
    .contactInfoIconBox {
        margin: 0 auto;
    }
    .mainContactInfo {
        height: auto;
        align-items: center;
        justify-content: center;
        padding-top: 5px;
        padding-left: 0;
    }   
    .contactInfo {
        height: auto;
        align-items: center;
        justify-content: center;
        gap: 30px 0;
    }
    .contactInfoItem {
        flex-direction: column;
        align-items: center;
    }   
    .socialmeidas {
        align-items: center;
        justify-content: center;
        gap: 20px;
    }
}


</style>