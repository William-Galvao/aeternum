<script setup>
import { ref } from 'vue';

const isTop = ref(true)
const mobileMenuActive = ref(false)
const emit = defineEmits(['selectedMenu'])


window.addEventListener('scroll', () => {
    if (window.scrollY !== 0) {
        isTop.value = false
    } else {
        isTop.value = true
    }
})

const navOptions = [
    { TITLE: "Project Insights", ELEMENT: "projectInsights" },
    { TITLE: "User Journey", ELEMENT: "userJourney" },
    { TITLE: "Meet Our Squad", ELEMENT: "meetOurSquad" },
    { TITLE: "Be a Beta Insider", ELEMENT: "beABetaInsider" },
    { TITLE: "Get in Touch", ELEMENT: "getinTouch" }
]


</script>

<template>
    <header
        class="fixed top-0 w-full flex px-4 lg:px-8 justify-between items-center h-24 z-50 transition duration-300 opacity-90"
        :class="isTop ? 'bg-transparent' : 'bg-black'">
        <div @click="$emit('selectedMenu', 'hero')" class="flex gap-x-2 items-end cursor-pointer animate__animated animate__backInLeft animate__slow">
            <img src="../assets/aeternum_logo.png" class="w-10" />
            <h1
                class="text-transparent text-center text-xl bg-gradient-to-r from-[#069f60] to-[#058dd8] bg-clip-text font-comfortaa">
                Aeternum
            </h1>
        </div>
        <ul class="hidden lg:flex gap-x-8 items-center animate__animated animate__fadeIn">
            <template v-for="option in navOptions">
                <li @click="$emit('selectedMenu', option.ELEMENT)"
                    class="cursor-pointer text-white text-xl transition duration-300 hover:scale-105">{{ option.TITLE }}
                </li>
            </template>
        </ul>
        <fa @click="mobileMenuActive = !mobileMenuActive" class="block lg:hidden text-xl text-white p-1"
            :icon="mobileMenuActive ? 'x' : 'bars'" />

    </header>
    <Transition enter-active-class="animate__animated animate__fadeInDown"
        leave-active-class="animate__animated animate__fadeOutUp">
        <ul v-if="mobileMenuActive"
            class="bg-black fixed top-0 pt-24 w-full h-screen z-40 lg:hidden flex flex-col gap-y-2 items-start">
            <template v-for="option in navOptions">
                <li @click="() => { $emit('selectedMenu', option.ELEMENT); mobileMenuActive = false }"
                    class="cursor-pointer text-white text-xl transition duration-300 hover:scale-105 p-4 border-b border-white w-full">
                    {{ option.TITLE }}</li>
            </template>
        </ul>
    </Transition>
</template>