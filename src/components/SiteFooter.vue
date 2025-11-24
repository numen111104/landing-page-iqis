<script setup>
import { MapPinIcon, PhoneIcon, EnvelopeIcon } from '@heroicons/vue/24/solid';

// Anda bisa menyesuaikan data kontak di bawah ini sesuai alamat asli IQIS
const contactInfo = {
    address: " Jl. Taman Bunga Sudiang No.2, Laikang",
    phone: "+6281341311314",
    email: "info@iqis.sch.id",
    maps: "https://maps.app.goo.gl/ZzYBZqB1SpMrGdYp8"
};
</script>

<template>
    <footer class="bg-iqis-green text-white pt-12 pb-6 border-t-4 border-iqis-yellow mt-auto">
        <div class="container mx-auto px-4">

            <div
                class="flex flex-col md:flex-row justify-between items-center md:items-start gap-8 text-center md:text-left">

                <div class="max-w-xs flex flex-col items-center md:items-start">

                    <div class="flex flex-col md:flex-row items-center gap-3 mb-4 md:mb-2">
                        <img src="../assets/logo.png" class="w-16 h-16 md:w-14 md:h-14 object-contain" alt="Logo IQIS">

                        <div class="flex flex-col items-center md:items-start">
                            <h3 class="font-heading font-bold text-xl md:text-2xl mb-1 text-white">IBNUL QAYYIM</h3>
                            <p class="text-iqis-yellow font-medium text-sm tracking-widest uppercase">
                                Islamic School
                            </p>
                        </div>
                    </div>

                    <p class="text-sm text-white/80 leading-relaxed">
                        Mewujudkan generasi Rabbani yang unggul dalam Imtaq dan Iptek berlandaskan Al-Qur'an dan Sunnah.
                    </p>
                </div>

                <div class="flex flex-col items-center md:items-start space-y-3 text-sm text-white/90">
                    <h4 class="font-bold text-iqis-yellow mb-3">Hubungi Kami</h4>

                    <a :href="contactInfo.maps" target="_blank"
                        class="flex items-center gap-3 group transition-colors duration-300 hover:text-iqis-yellow">
                        <div
                            class="w-8 h-8 rounded-full bg-white/10 flex items-center justify-center transition-colors duration-300 group-hover:bg-iqis-yellow group-hover:text-iqis-green">
                            <MapPinIcon class="w-4 h-4" />
                        </div>
                        <span>{{ contactInfo.address }}</span>
                    </a>

                    <a :href="`https://wa.me/${contactInfo.phone.replace(/[^0-9]/g, '')}`" target="_blank"
                        class="flex items-center gap-3 group transition-colors duration-300 hover:text-iqis-yellow">
                        <div
                            class="w-8 h-8 rounded-full bg-white/10 flex items-center justify-center transition-colors duration-300 group-hover:bg-iqis-yellow group-hover:text-iqis-green">
                            <PhoneIcon class="w-4 h-4" />
                        </div>
                        <span>{{ contactInfo.phone }}</span>
                    </a>

                    <a :href="`mailto:${contactInfo.email}`"
                        class="flex items-center gap-3 group transition-colors duration-300 hover:text-iqis-yellow">
                        <div
                            class="w-8 h-8 rounded-full bg-white/10 flex items-center justify-center transition-colors duration-300 group-hover:bg-iqis-yellow group-hover:text-iqis-green">
                            <EnvelopeIcon class="w-4 h-4" />
                        </div>
                        <span>{{ contactInfo.email }}</span>
                    </a>
                </div>

            </div>

            <div class="border-t border-white/10 mt-10 pt-6">
                <div class="flex flex-col md:flex-row justify-between items-center text-xs text-white/60">
                    <p class="mb-2 md:mb-0">
                        &copy; {{ new Date().getFullYear() }} Yayasan Ibnul Qayyim. All Rights Reserved.
                    </p>
                    <!-- <p>
                        Designed with <span class="text-red-500 animate-pulse">❤</span> using Vue.js & Tailwind CSS
                    </p> -->
                </div>
            </div>

        </div>
    </footer>
</template>