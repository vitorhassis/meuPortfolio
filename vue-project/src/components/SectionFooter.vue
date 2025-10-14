<script setup>
import iconInstagram from "@/assets/iconInstagram.svg";
import iconLinkedin from "@/assets/iconLinkedin.svg";
import iconGithub from "@/assets/iconGithub.svg";
import iconCv from "@/assets/iconCv.svg";
</script>

<template>
    <section class="flex justify-between items-center ">

        <div class="flex gap-6 items-center">
            <a href="https://www.instagram.com/ass.vitor/" target="_blank">
            <img :src="iconInstagram" alt="instagram" class="w-7 h-7 hover:scale-110 transition-transform duration-300">
        </a>
        <a href="https://github.com/vitorhassis" target="_blank">
            <img :src="iconGithub" alt="github" class="w-7 h-7 hover:scale-110 transition-transform duration-300">
        </a>
        <a href="www.linkedin.com/in/vitor-hugo-assis" target="_blank">
            <img :src="iconLinkedin" alt="linkedin" class="w-10 h-10 hover:scale-110 transition-transform duration-300">
        </a>
        <a href="www.linkedin.com/in/vitor-hugo-assis" target="_blank">
            <img :src="iconCv" alt="icon curriculo" class="w-7 h-7 hover:scale-110 transition-transform duration-300">
        </a>
        </div>

        <div>
            <p>2025 © Vitor Assis</p>
        </div>
        
    </section>

</template>
