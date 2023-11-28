<template>
    <div class="absolute top-0 left-0 w-screen">
        <div class="navbar p-5 lg:px-16 2xl:px-20 lg:py-6 2xl:py-14 flex flex-row items-center justify-between">
            <span class="navbar-title font-semibold text-xl lg:text-2xl xl:text-4xl 2xl:text-6xl"><a href="/">Crypto</a></span>
            <div class="navbar-group-btns hidden md:block">
                <ul v-if="route.name == 'home'" class="flex gap-3 text-xs 2xl:gap-6 lg:text-lg xl:text-xl 2xl:text-3xl">
                <li><a href="#watch">Watch</a></li>
                <li><a href="#features">Features</a></li>
                <li><a href="#feedback">Feedback</a></li>
                </ul>
            </div>
            <button class="navbar-btn bg-red-600 text-white px-5 lg:px-7 xl:px-7 2xl:px-10 py-2 2xl:py-4 rounded-full text-xs lg:text-lg xl:text-xl 2xl:text-3xl">Get Started</button>
        </div>
    </div>
</template>

<script setup>
import { useRoute } from 'vue-router'

const route = useRoute();
</script>

<style>

</style>