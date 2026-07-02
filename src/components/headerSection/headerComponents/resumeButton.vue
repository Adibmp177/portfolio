<script setup>
// import { defineEmits } from "vue";

// const emits = defineEmits(['toResume']);

// function openResume() {
//     emits('toResume');
// }

</script>

<template>

    <button class="resumeButton">
        Download CV
    </button>

</template>

<style scoped>

.resumeButton {
    appearance: none;
    padding: 6px 34px;
    border-radius: 4px;
    color: #fff;
    font-size: 18px;
    cursor: pointer;
    background-size: 255% auto;
    background-image: linear-gradient(to right, #1426CD 0%, #E91E1E 50%, #1426CD 100%);
    border: none;
    outline: none;
    transition: 0.45s;
}

.resumeButton:hover {
    background-position: 100% 50%;
}


</style>