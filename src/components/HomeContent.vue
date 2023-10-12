<script setup>

function scrollToDiv(id) {
    const div = document.getElementById(id);
    div.scrollIntoView({ behavior: "smooth" });
}

</script>

<template>
    <div class="animate__animated animate__fadeIn">
        <div class="h-screen bg-[url('assets/hero_background.jpg')] bg-cover bg-center flex px-8">
            <div class="lg:w-1/2 flex flex-col gap-y-8 justify-center animate__animated animate__fadeIn">
                <p class="text-white text-5xl lg:text-7xl font-bold">
                    Bridging Generations Through Legacy
                </p>
                <button @click="scrollToDiv('learnmore')"
                    class="self-start h-14 px-4 bg-gradient-to-r from-[#069f60] to-[#058dd8] text-white text-xl lg:text-2xl rounded transition duration-300 hover:scale-105 shadow-lg">
                    Learn More
                </button>
            </div>
        </div>
        <div class="flex flex-col-reverse lg:flex-row bg-black" id="learnmore">
            <div class="lg:w-1/2 flex justify-center items-center">
                <img src="../assets/photo_album.jpg" class="grayscale p-1" />
            </div>
            <div class="lg:w-1/2 flex flex-col justify-center items-start gap-y-4 text-white p-8">
                <p class="text-4xl">
                    Our mission at
                    <span class="text-transparent text-center bg-gradient-to-r from-[#069f60] to-[#058dd8] bg-clip-text">
                        Aeternum
                    </span>
                    is to preserve personal legacies and connect generations of families.
                </p>

                <p class="text-xl">
                    We believe in the power of storytelling, and the importance of preserving the wisdom and experiences of
                    the past. We strive to capture personal legacies, keeping them alive and tangible for future
                    generations. Utilizing advanced technology, we build bridges between generations, fostering a deeper
                    understanding and connection within families. Our commitment to safeguarding these precious narratives
                    ensures they are never lost, fostering a continuity of knowledge and wisdom that transcends time.
                </p>

                <p class="text-2xl">
                    Welcome to
                    <span class="text-transparent text-center bg-gradient-to-r from-[#069f60] to-[#058dd8] bg-clip-text">
                        Aeternum
                    </span>
                    , where your legacy lives on.
                </p>
            </div>
        </div>
        <div class="bg-gradient-to-r from-[#069f60] to-[#058dd8] p-1 m-8">
            <div class="flex flex-col justify-center items-center gap-y-8 text-white bg-black p-8 text-center">
                <p class="text-xl lg:text-2xl">
                    <span class="text-transparent text-center bg-gradient-to-r from-[#069f60] to-[#058dd8] bg-clip-text">
                        Aeternum
                    </span>
                    is currently in its early development stage and we need your help in shaping its design.
                </p>
                <p class="text-xl lg:text-2xl">
                    Please
                    support us by completing our survey!
                </p>
                <button
                    class="h-14 px-4 bg-gradient-to-r from-[#069f60] to-[#058dd8] text-white text-xl lg:text-3xl rounded transition duration-300 hover:scale-105 shadow-lg">
                    Complete the survey
                </button>
            </div>
        </div>
    </div>
</template>