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
    { TITLE: "Home", ELEMENT: "Home" },
    { TITLE: "About Us", ELEMENT: "About Us" },
    { TITLE: "Progress Tracker", ELEMENT: "Progress Tracker" },
    { TITLE: "User Stories", ELEMENT: "User Stories" },
    { TITLE: "Aeternum Insights", ELEMENT: "Aeternum Insights" },
    { TITLE: "Get in Touch", ELEMENT: "Get in Touch" }
]


</script>

<template>
    <header
        class="fixed top-0 w-full flex px-4 lg:px-8 justify-between items-center h-24 z-50 transition duration-300 opacity-90"
        :class="isTop ? 'bg-transparent' : 'bg-black'">
        <div class="flex gap-x-2 items-center cursor-pointer animate__animated animate__backInLeft animate__slow" @click="$emit('selectedMenu', 'Home')">
            <img src="../assets/aeternum_logo.png" class="w-12" />
            <h1 class="text-transparent text-center text-3xl bg-gradient-to-r from-[#069f60] to-[#058dd8] bg-clip-text">
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
        <fa @click="mobileMenuActive = !mobileMenuActive" class="block lg:hidden border rounded p-2 text-white text-2xl"
            icon="bars" />

    </header>
    <Transition enter-active-class="animate__animated animate__fadeInLeft"
        leave-active-class="animate__animated animate__fadeOutLeft">
        <ul v-if="mobileMenuActive"
            class="bg-black fixed top-24 w-full z-50 lg:hidden flex flex-col gap-y-2 items-start opacity-90">
            <template v-for="option in navOptions">
                <li @click="() => {$emit('selectedMenu', option.ELEMENT); mobileMenuActive = false}"
                    class="cursor-pointer text-white text-xl transition duration-300 hover:scale-105 p-4 border-b border-white w-full">
                    {{ option.TITLE }}</li>
            </template>
        </ul>
    </Transition>
</template>