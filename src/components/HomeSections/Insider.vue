<script setup>

import { ref } from 'vue'
import { doc, setDoc } from "firebase/firestore";
import { db } from '@/firebase';
import {useToast} from 'vue-toast-notification';
import 'vue-toast-notification/dist/theme-sugar.css';

const $toast = useToast();

const userEmail = ref('')
const alreadySubscribed = ref(localStorage.getItem("aeternumBeta"))
const loading = ref(false)


function validateInfos() {

if(!userEmail.value) return { status: false, message: "Please enter your email." }

const emailRegex = /^[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,}$/i
if (!emailRegex.test(userEmail.value)) return { status: false, message: "The provided email does not exist." }

return { status: true }
}


async function subscribeBeta() {
    loading.value = true

    if (!validateInfos().status) {
        loading.value = false
        $toast.error(validateInfos().message)
        return
    }

    await setDoc(doc(db, "SUBS", userEmail.value), {
        EMAIL: userEmail.value
    }).then(() => {
        loading.value = false
        localStorage.setItem("aeternumBeta", userEmail.value)
        alreadySubscribed.value = localStorage.getItem("aeternumBeta")
    }).catch((error) => {
        loading.value = false
        console.error(error)
    })

}



</script>

<template>
    <div class="bg-[#f4f4f4] w-full py-24 flex justify-center px-4">

        <div class="lg:w-2/3 flex justify-between items-center bg-[#f4f4f4]">

            <div class="lg:w-1/3 flex flex-col gap-y-6">
                <p class="text-2xl">
                    We are excited to announce that <span
                        class="text-transparent text-center bg-gradient-to-r from-[#069f60] to-[#058dd8] bg-clip-text font-comfortaa">
                        Aeternum
                    </span> is entering its beta phase, and we would like to invite you to
                    be a part of this exciting journey.
                </p>

                <div v-if="!alreadySubscribed" class="flex flex-col gap-y-4">
                    <p class="text-xl">
                        Please provide your email:
                    </p>
                    <input v-model="userEmail" class="h-12 rounded w-full focus:outline-none p-2">

                    <button @click="subscribeBeta"
                        class="flex w-60 justify-center items-center h-14 w-fit px-4 bg-gradient-to-r from-[#069f60] to-[#058dd8] text-white lg:text-xl font-semibold rounded transition duration-300 hover:scale-105 shadow-lg">
                        <span v-if="!loading">Subscribe to the beta</span>
                        <svg v-else aria-hidden="true"
                            class="w-8 h-8 text-white animate-spin fill-[#07969d]"
                            viewBox="0 0 100 101" fill="none" xmlns="http://www.w3.org/2000/svg">
                            <path
                                d="M100 50.5908C100 78.2051 77.6142 100.591 50 100.591C22.3858 100.591 0 78.2051 0 50.5908C0 22.9766 22.3858 0.59082 50 0.59082C77.6142 0.59082 100 22.9766 100 50.5908ZM9.08144 50.5908C9.08144 73.1895 27.4013 91.5094 50 91.5094C72.5987 91.5094 90.9186 73.1895 90.9186 50.5908C90.9186 27.9921 72.5987 9.67226 50 9.67226C27.4013 9.67226 9.08144 27.9921 9.08144 50.5908Z"
                                fill="currentColor" />
                            <path
                                d="M93.9676 39.0409C96.393 38.4038 97.8624 35.9116 97.0079 33.5539C95.2932 28.8227 92.871 24.3692 89.8167 20.348C85.8452 15.1192 80.8826 10.7238 75.2124 7.41289C69.5422 4.10194 63.2754 1.94025 56.7698 1.05124C51.7666 0.367541 46.6976 0.446843 41.7345 1.27873C39.2613 1.69328 37.813 4.19778 38.4501 6.62326C39.0873 9.04874 41.5694 10.4717 44.0505 10.1071C47.8511 9.54855 51.7191 9.52689 55.5402 10.0491C60.8642 10.7766 65.9928 12.5457 70.6331 15.2552C75.2735 17.9648 79.3347 21.5619 82.5849 25.841C84.9175 28.9121 86.7997 32.2913 88.1811 35.8758C89.083 38.2158 91.5421 39.6781 93.9676 39.0409Z"
                                fill="currentFill" />
                        </svg>
                    </button>
                </div>
                <div v-else class="bg-gradient-to-b from-[#069f60] to-[#058dd8] pl-1 animate__animated animate__fadeIn">
                    <div class="flex flex-col gap-y-4 bg-[#f4f4f4] pl-2">
                        <p class="text-xl">We wish to express our sincere gratitude for your participation in <span
                                class="text-transparent text-center bg-gradient-to-r from-[#069f60] to-[#058dd8] bg-clip-text font-comfortaa">
                                Aeternum
                            </span>'s beta program.</p>
                        <p class="text-xl">Please expect to receive an email notification at <span class="font-bold">{{alreadySubscribed}}</span> when everything is set to go.</p>
                    </div>
                </div>
            </div>
            <div class="lg:w-2/3 hidden lg:block">
                <img src="../../assets/young-mom-holding-her-baby.jpg" class="rounded" />
            </div>

    </div>

</div></template>