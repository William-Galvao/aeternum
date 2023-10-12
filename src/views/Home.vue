<script setup>
import { ref } from 'vue'
import MyHeader from '../components/MyHeader.vue';
import MyFooter from '../components/MyFooter.vue';
import HomeContent from '../components/HomeContent.vue';
import UnderConstruction from '../components/UnderConstruction.vue';

const contentActive = ref('Home')

</script>



<template>
    <MyHeader @selectedMenu="(element) => contentActive = element"/>
        
    <HomeContent v-if="contentActive === 'Home'" />

    <UnderConstruction v-else/>

    <MyFooter />
</template>