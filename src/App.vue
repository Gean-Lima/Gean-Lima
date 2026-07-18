<script setup>
import { onBeforeUnmount, onMounted, ref } from 'vue';
import Header from '@/components/layout/Header.vue';
import Hero from '@/components/layout/Hero.vue';
import Stacks from '@/components/layout/Stacks.vue';

const activeCategory = ref('landing');
let animationFrame;

function moveSpotlight(event) {
    if (animationFrame) cancelAnimationFrame(animationFrame);

    animationFrame = requestAnimationFrame(() => {
        const x = `${(event.clientX / window.innerWidth) * 100}%`;
        const y = `${(event.clientY / window.innerHeight) * 100}%`;
        document.documentElement.style.setProperty('--pointer-x', x);
        document.documentElement.style.setProperty('--pointer-y', y);
    });
}

onMounted(() => window.addEventListener('pointermove', moveSpotlight, { passive: true }));

onBeforeUnmount(() => {
    window.removeEventListener('pointermove', moveSpotlight);
    if (animationFrame) cancelAnimationFrame(animationFrame);
});
</script>

<template>
    <div style="padding: 12px;">
        <div class="portfolio-shell">
            <div class="ambient ambient--one" aria-hidden="true"></div>
            <div class="ambient ambient--two" aria-hidden="true"></div>
    
            <Header v-model="activeCategory" />
    
            <main>
                <Hero :category="activeCategory" />
                <Stacks />
            </main>
        </div>
    </div>
</template>
