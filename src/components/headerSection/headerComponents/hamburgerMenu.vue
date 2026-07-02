<script setup>
import { defineEmits, defineProps } from "vue";


const props = defineProps(['menuHandler']);
const emits = defineEmits(['toggleMenu'])

function toggleMenu() {
    emits('toggleMenu');
}


</script>

<template>

    <div class="hamburgerMenu--wrapper">
        <div class="hamburger" :class="{'is-active': props.menuHandler}" @click="toggleMenu($event.currentTarget)" id="hamburger-6">
          <span class="line"></span>
          <span class="line"></span>
          <span class="line"></span>
        </div>
    </div>


</template>

<style>

.hamburgerMenu--wrapper {
  display: none;
  align-items: center;
  justify-content: center;
}

.hamburger .line{
  width: 30px;
  height: 3px;
  background-color: var(--main-txt);
  display: block;
  margin: 5px auto;
  border-radius: 150px;
  -webkit-transition: all 0.2s ease-in-out;
  -o-transition: all 0.2s ease-in-out;
  transition: all 0.2s ease-in-out;
}

.hamburger:hover{
  cursor: pointer;
}

#hamburger-6.is-active{
  -webkit-transition: all 0.2s ease-in-out;
  -o-transition: all 0.2s ease-in-out;
  transition: all 0.2s ease-in-out;
  /* -webkit-transition-delay: 0.4s; */
  /* -o-transition-delay: 0.4s; */
  /* transition-delay: 0.4s; */
  -webkit-transform: rotate(45deg);
  -ms-transform: rotate(45deg);
  -o-transform: rotate(45deg);
  transform: rotate(45deg);
}

#hamburger-6.is-active .line:nth-child(2){
  width: 0px;
}

#hamburger-6.is-active .line:nth-child(1),
#hamburger-6.is-active .line:nth-child(3){
  -webkit-transition-delay: 0.2s;
  -o-transition-delay: 0.2s;
  transition-delay: 0.2s;
}

#hamburger-6.is-active .line:nth-child(1){
  -webkit-transform: translateY(13px);
  -ms-transform: translateY(13px);
  -o-transform: translateY(13px);
  transform: translateY(13px);
}

#hamburger-6.is-active .line:nth-child(3){
  -webkit-transform: translateY(-13px) rotate(90deg);
  -ms-transform: translateY(-13px) rotate(90deg);
  -o-transform: translateY(-13px) rotate(90deg);
  transform: translateY(-3px) rotate(90deg);
}

@media screen and (max-width: 991px) {
    .hamburgerMenu--wrapper {
        display: flex;
        
    } 
}
@media screen and (max-width: 768px) {
  .hamburger {
    transform: scale(0.8);
  }
}

</style>