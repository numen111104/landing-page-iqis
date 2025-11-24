<script setup>
import HeroSection from './components/HeroSection.vue';
import UnitCard from './components/UnitCard.vue';
import SiteFooter from './components/SiteFooter.vue';

// Import Assets (Pastikan path benar)
import kbitLogo from './assets/kbit.png';
import tkitLogo from './assets/tkit.png';
import sditLogo from './assets/sdit.png';
import smpitLogo from './assets/smpit.png';
import smkitLogo from './assets/smkit.png';

const unitLinks = [
  { name: 'KBIT Ibnul Qayyim', icon: kbitLogo, bio: 'https://linkbio.co/kbitibnulqayyim', ig: 'https://instagram.com/kbitibnulqayyim' },
  { name: 'TKIT Ibnul Qayyim', icon: tkitLogo, bio: 'https://linktr.ee/tkitibnulqayyim', ig: 'https://instagram.com/tkitibnulqayyim' },
  { name: 'SDIT Ibnul Qayyim', icon: sditLogo, bio: 'https://linktr.ee/sditibnulqayyim', ig: 'https://instagram.com/sditibnulqayyim' },
  { name: 'SMPIT Ibnul Qayyim', icon: smpitLogo, bio: 'https://linktr.ee/smpitibnulqayyim', ig: 'https://instagram.com/smpitibnulqayyim' },
  { name: 'SMKIT Ibnul Qayyim', icon: smkitLogo, bio: 'https://linktr.ee/smkitibnulqayyim', ig: 'https://instagram.com/smkitibnulqayyim' }
];
</script>

<template>

  <div class="min-h-screen flex flex-col font-sans bg-[#F3F6F4] overflow-x-hidden">
    <HeroSection />
    <main class="grow container mx-auto px-4 py-16 -mt-10 relative z-20">
      <div class="absolute top-20 left-0 w-72 h-72 bg-iqis-green/10 rounded-full blur-[80px] -z-10 animate-pulse"></div>
      <div class="absolute bottom-20 right-0 w-96 h-96 bg-iqis-yellow/10 rounded-full blur-[100px] -z-10"></div>
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8 max-w-6xl mx-auto">
        <UnitCard v-for="(unit, index) in unitLinks" :key="index" :unitName="unit.name" :source="unit.icon"
          :bioLink="unit.bio" :igLink="unit.ig" :class="{ 'lg:col-start-2': index === 4 && unitLinks.length === 5 }" />
      </div>
    </main>
    <SiteFooter />
  </div>

</template>
