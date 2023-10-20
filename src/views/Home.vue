<script setup>
import { ref } from 'vue'
import MyHeader from '../components/MyHeader.vue';
import MyFooter from '../components/MyFooter.vue';
import HomeContent from '../components/HomeContent.vue';
import UnderConstruction from '../components/UnderConstruction.vue';

const contentActive = ref('Home')

function scrollToDiv(id) {
    const div = document.getElementById(id);
    div.scrollIntoView({ behavior: "smooth" });
}

</script>



<template>
    <MyHeader @selectedMenu="(element) => scrollToDiv(element)" />

    <HomeContent v-if="contentActive === 'Home'" />

    <UnderConstruction v-else />

    <MyFooter />
</template>