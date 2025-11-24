<script setup>
import GeometricCanvas from './GeometricCanvas.vue';
import logoUrl from '../assets/logo.png'; 
</script>

<template>
    <section class="relative bg-iqis-green overflow-hidden text-center py-12 md:py-16 px-4">
        <GeometricCanvas />

        <div class="relative z-10 flex flex-col items-center">
            <img :src="logoUrl" alt="Logo IQIS" class="w-24 md:w-32 h-auto mb-6 drop-shadow-md">

            <h1 class="font-heading text-2xl md:text-4xl font-bold text-white mb-2 tracking-wide">
                IBNUL QAYYIM ISLAMIC SCHOOL
            </h1>

            <div class="w-24 h-1 bg-iqis-yellow rounded-full mb-4"></div>

            <p class="text-iqis-yellow font-semibold text-lg md:text-xl">
                Sekolah Tahfidz dan Bahasa Asing
            </p>

            <p class="text-white text-opacity-90 mt-4 max-w-md text-sm md:text-base">
                Portal resmi tautan informasi dan media sosial seluruh unit pendidikan di bawah naungan IQIS.
            </p>
        </div>
    </section>
</template>