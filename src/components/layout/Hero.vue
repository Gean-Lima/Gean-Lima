<script setup>
import { computed } from 'vue';
import IconMark from '@/components/ui/IconMark.vue';

const props = defineProps({
    category: {
        type: String,
        required: true,
    },
});

const content = {
    home: {
        kicker: 'Desenvolvedor Full-stack',
        title: ['Gean Lima'],
        description:
            'Desenvolvedor focado em criar aplicações web e mobile consistentes, unindo design intuitivo e arquitetura robusta.',
    },
    landing: {
        kicker: 'Design & desenvolvimento',
        title: ['Páginas que', 'fazem acontecer.'],
        description:
            'Landing pages rápidas, autorais e construídas para transformar atenção em resultado.',
    },
    systems: {
        kicker: 'Produto & arquitetura',
        title: ['Complexidade,', 'sem complicação.'],
        description:
            'Sistemas web consistentes para organizar processos, dados e decisões do dia a dia.',
    },
    apps: {
        kicker: 'Mobile & experiência',
        title: ['Ideias que cabem', 'na palma da mão.'],
        description:
            'Aplicativos leves e diretos, desenhados para serem úteis desde o primeiro toque.',
    },
};

const stackItems = [
    { id: 'laravel', label: 'Laravel', icon: 'laravel' },
    { id: 'vue', label: 'Vue.js', icon: 'vue' },
    { id: 'nuxt', label: 'Nuxt', icon: 'nuxt' },
    { id: 'flutter', label: 'Flutter', icon: 'flutter' },
    { id: 'php', label: 'PHP', icon: 'php' },
    { id: 'mysql', label: 'MySQL', icon: 'mysql' },
];

const current = computed(() => content[props.category] ?? content.home);
const isHome = computed(() => props.category === 'home');
</script>

<template>
    <section class="hero" :class="{ 'hero--home': isHome }" aria-live="polite">
        <Transition name="category" mode="out-in">
            <div :key="category" class="hero__copy">
                <p class="hero__kicker">{{ current.kicker }}</p>

                <h1>
                    <span v-for="line in current.title" :key="line">{{ line }}</span>
                </h1>

                <div class="hero__intro">
                    <div class="hero__intro-text">
                        <p>{{ current.description }}</p>

                        <div v-if="isHome" class="hero__simple-details">
                            <div class="hero__detail">
                                <span class="hero__detail-label">Experiência</span>
                                <span class="hero__detail-value">2018-Agora · Desenvolvimento full-stack</span>
                            </div>

                            <div class="hero__detail">
                                <span class="hero__detail-label">Stack</span>
                                <div class="hero__stack-list" role="list" aria-label="Principais stacks">
                                    <span v-for="stack in stackItems" :key="stack.id" class="stack-pill" role="listitem">
                                        <IconMark :name="stack.icon" />
                                        <span>{{ stack.label }}</span>
                                    </span>
                                </div>
                            </div>
                        </div>
                    </div>

                    <a
                        class="hero__cta"
                        href="https://www.linkedin.com/in/gean-lima-775b491a2/"
                        target="_blank"
                        rel="noopener noreferrer"
                    >
                        Iniciar um projeto
                        <IconMark name="whatsapp" />
                    </a>
                </div>
            </div>
        </Transition>

        <Transition name="tech-visual" mode="out-in">
            <div v-if="isHome" class="tech-visual" aria-hidden="true">
                <svg viewBox="0 0 480 320" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <defs>
                        <pattern id="grid" width="40" height="40" patternUnits="userSpaceOnUse">
                            <path d="M40 0L0 0 0 40" fill="none" stroke="rgba(238,241,232,0.04)" stroke-width="0.5" />
                        </pattern>
                        <radialGradient id="fade" cx="50%" cy="50%" r="50%">
                            <stop offset="0%" stop-color="white" />
                            <stop offset="100%" stop-color="white" stop-opacity="0" />
                        </radialGradient>
                        <mask id="fade-mask">
                            <rect width="480" height="320" fill="url(#fade)" />
                        </mask>
                    </defs>

                    <rect width="480" height="320" fill="url(#grid)" mask="url(#fade-mask)" />

                    <g stroke="rgba(199,255,73,0.12)" stroke-width="1" fill="none">
                        <polyline points="74,170 130,170 150,132 214,132 238,170 300,170" class="circuit circuit--1" />
                        <polyline points="182,212 246,212 266,170 330,170 354,212 414,212" class="circuit circuit--2" />
                        <polyline points="142,92 182,92 200,132 214,132" class="circuit circuit--3" />
                        <polyline points="300,170 322,132 378,132 398,92" class="circuit circuit--4" />
                    </g>

                    <g>
                        <circle cx="130" cy="170" r="3" fill="rgba(199,255,73,0.5)" class="node node--1" />
                        <circle cx="214" cy="132" r="3" fill="rgba(199,255,73,0.55)" class="node node--2" />
                        <circle cx="300" cy="170" r="4" fill="rgba(199,255,73,0.75)" class="node node--3" />
                        <circle cx="182" cy="92" r="2.5" fill="rgba(199,255,73,0.35)" class="node node--4" />
                        <circle cx="398" cy="92" r="2.5" fill="rgba(199,255,73,0.35)" class="node node--5" />
                        <circle cx="246" cy="212" r="2.5" fill="rgba(199,255,73,0.35)" class="node node--6" />
                        <circle cx="354" cy="212" r="2.5" fill="rgba(199,255,73,0.35)" class="node node--7" />
                    </g>

                    <circle cx="300" cy="170" r="10" fill="none" stroke="rgba(199,255,73,0.18)" stroke-width="0.6" class="pulse pulse--1" />
                    <circle cx="300" cy="170" r="18" fill="none" stroke="rgba(199,255,73,0.1)" stroke-width="0.6" class="pulse pulse--2" />
                    <circle cx="300" cy="170" r="30" fill="none" stroke="rgba(199,255,73,0.06)" stroke-width="0.6" class="pulse pulse--3" />

                    <circle r="2" fill="var(--accent)" class="packet packet--1">
                        <animateMotion
                            dur="3.8s"
                            repeatCount="indefinite"
                            path="M74,170 L130,170 L150,132 L214,132 L238,170 L300,170"
                        />
                    </circle>

                    <circle r="1.8" fill="var(--accent)" class="packet packet--2">
                        <animateMotion
                            dur="4.2s"
                            repeatCount="indefinite"
                            begin="1.1s"
                            path="M182,212 L246,212 L266,170 L330,170 L354,212 L414,212"
                        />
                    </circle>

                    <text x="86" y="110" fill="rgba(199,255,73,0.12)" font-family="'kodemono', monospace" font-size="11" class="code-sym code-sym--1">&lt;/&gt;</text>
                    <text x="352" y="108" fill="rgba(199,255,73,0.1)" font-family="'kodemono', monospace" font-size="10" class="code-sym code-sym--2">{ }</text>
                    <text x="108" y="262" fill="rgba(199,255,73,0.08)" font-family="'kodemono', monospace" font-size="9" class="code-sym code-sym--3">fn()</text>
                    <text x="378" y="266" fill="rgba(199,255,73,0.08)" font-family="'kodemono', monospace" font-size="10" class="code-sym code-sym--4">async</text>

                    <polygon points="300,146 318,158 318,182 300,194 282,182 282,158" fill="none" stroke="rgba(199,255,73,0.25)" stroke-width="0.8" class="hex" />
                    <text x="300" y="172" text-anchor="middle" fill="rgba(199,255,73,0.6)" font-family="'kodemono', monospace" font-size="8" font-weight="600" class="hex-label">GL</text>
                </svg>
            </div>
        </Transition>
    </section>
</template>

<style lang="scss">
.hero {
    position: relative;
    min-height: 0;
    display: grid;
    grid-template-columns: 1fr;
    align-items: center;
    padding: clamp(0.6rem, 1.5vh, 1rem) 0;
}

.hero--home {
    grid-template-columns: minmax(0, 1.2fr) minmax(220px, 0.8fr);
    gap: clamp(2rem, 5vw, 5rem);
    padding: clamp(1.25rem, 3vh, 3rem) 0;
}

.hero__copy {
    min-width: 0;
}

.hero__kicker {
    margin: 0 0 clamp(0.5rem, 1vh, 0.8rem);
    color: var(--muted);
    font: 400 clamp(0.58rem, 0.7vw, 0.72rem)/1 'kodemono', monospace;
    letter-spacing: 0.12em;
    text-transform: uppercase;
}

.hero--home .hero__kicker {
    margin-bottom: clamp(1rem, 2vh, 1.7rem);
}

.hero__kicker span {
    margin-right: 0.75rem;
    color: var(--accent);
}

.hero h1 {
    margin: 0;
    color: var(--ink);
    font: 400 clamp(1.6rem, 3.5vw, 3.5rem)/0.92 'open-sans', sans-serif;
    letter-spacing: -0.05em;
}

.hero--home h1 {
    font-size: clamp(2.65rem, 6.5vw, 7.1rem);;
    line-height: 0.89;
    letter-spacing: -0.06em;
}

.hero h1 span {
    display: block;
}

.hero--home h1 span:only-child {
    color: var(--ink);
}

.hero span:last-child {
    color: transparent;
    -webkit-text-stroke: 1px rgba(238, 241, 232, 0.55);
}

.hero--home span:only-child {
    color: var(--ink);
    -webkit-text-stroke: 0;
}

.hero__intro {
    margin-top: clamp(1rem, 2.2vh, 1.4rem);
    padding-top: clamp(0.95rem, 1.8vh, 1.2rem);
    display: grid;
    grid-template-columns: minmax(0, 1fr) auto;
    gap: 1rem;
    align-items: end;
    border-top: 1px solid var(--line);
}

.hero--home .hero__intro {
    margin-top: clamp(1.1rem, 2.5vh, 1.6rem);
    padding-top: clamp(1rem, 2vh, 1.4rem);
}

.hero__intro-text {
    min-width: 0;
}

.hero__intro-text p {
    max-width: 40ch;
    margin: 0;
    color: var(--muted-light);
    font: 400 0.82rem/1.7 'kodemono', monospace;
}

.hero__simple-details {
    margin-top: 1rem;
    display: grid;
    gap: 0.85rem;
}

.hero__detail {
    display: grid;
    gap: 0.45rem;
}

.hero__detail-label {
    color: var(--accent);
    font: 500 0.6rem/1 'kodemono', monospace;
    letter-spacing: 0.12em;
    text-transform: uppercase;
}

.hero__detail-value {
    color: var(--muted);
    font: 400 0.65rem/1.5 'kodemono', monospace;
    letter-spacing: 0.05em;
}

.hero__stack-list {
    display: flex;
    flex-wrap: wrap;
    gap: 0.45rem;
}

.stack-pill {
    display: inline-flex;
    align-items: center;
    gap: 0.4rem;
    padding: 0.36rem 0.55rem;
    border: 1px solid var(--line);
    border-radius: 999px;
    background: rgba(11, 13, 14, 0.45);
    color: var(--ink);
    font: 400 0.55rem/1 'kodemono', monospace;
    letter-spacing: 0.08em;
    text-transform: uppercase;
}

.stack-pill svg {
    width: 0.8rem;
    height: 0.8rem;
    color: var(--accent);
    flex: none;
}

.hero__cta {
    justify-self: end;
    display: inline-flex;
    align-items: center;
    gap: 0.55rem;
    padding: 0.85rem 1rem;
    border: 1px solid var(--line-strong);
    color: var(--ink);
    font: 500 0.68rem/1 'kodemono', monospace;
    letter-spacing: 0.08em;
    text-decoration: none;
    text-transform: uppercase;
    white-space: nowrap;
    transition: border-color 200ms ease, color 200ms ease, background 200ms ease, transform 200ms ease;
}

.hero__cta:hover {
    border-color: rgba(199, 255, 73, 0.28);
    color: var(--accent);
    background: rgba(199, 255, 73, 0.03);
    transform: translateY(-1px);
}

.hero__cta svg {
    width: 0.95rem;
    height: 0.95rem;
}

.tech-visual {
    justify-self: end;
    width: 100%;
    max-width: 480px;
    animation: tech-in 1s 300ms var(--ease-out) both;
}

.tech-visual svg {
    width: 100%;
    height: auto;
}

.circuit {
    stroke-dasharray: 360;
    stroke-dashoffset: 360;
    animation: draw-line 2s var(--ease-out) forwards;
}

.circuit--1 {
    animation-delay: 0.2s;
}

.circuit--2 {
    animation-delay: 0.55s;
}

.circuit--3 {
    animation-delay: 0.8s;
}

.circuit--4 {
    animation-delay: 1.05s;
}

.node {
    opacity: 0;
    animation: node-pop 420ms var(--ease-out) forwards;
}

.node--1 {
    animation-delay: 0.55s;
}

.node--2 {
    animation-delay: 0.75s;
}

.node--3 {
    animation-delay: 0.95s;
}

.node--4 {
    animation-delay: 1.05s;
}

.node--5 {
    animation-delay: 1.15s;
}

.node--6 {
    animation-delay: 1.25s;
}

.node--7 {
    animation-delay: 1.35s;
}

.pulse {
    animation: pulse-ring 3s ease-out infinite;
}

.pulse--2 {
    animation-delay: 0.6s;
}

.pulse--3 {
    animation-delay: 1.2s;
}

.packet {
    filter: drop-shadow(0 0 4px rgba(199, 255, 73, 0.6));
}

.code-sym {
    animation: sym-float 6s ease-in-out infinite;
}

.code-sym--2 {
    animation-delay: 1s;
}

.code-sym--3 {
    animation-delay: 1.8s;
}

.code-sym--4 {
    animation-delay: 2.5s;
}

.hex {
    animation: hex-pulse 4s ease-in-out infinite;
}

.category-enter-active,
.category-leave-active {
    transition: opacity 220ms var(--ease-out), transform 220ms var(--ease-out), filter 220ms var(--ease-out);
}

.category-enter-from,
.category-leave-to {
    opacity: 0;
    transform: translateY(6px);
    filter: blur(4px);
}

.tech-visual-enter-active,
.tech-visual-leave-active {
    transition: opacity 400ms ease, transform 400ms var(--ease-out);
}

.tech-visual-enter-from {
    opacity: 0;
    transform: scale(0.9);
}

.tech-visual-leave-to {
    opacity: 0;
    transform: scale(0.95);
}

@keyframes draw-line {
    to {
        stroke-dashoffset: 0;
    }
}

@keyframes node-pop {
    from {
        opacity: 0;
        transform: scale(0);
    }

    to {
        opacity: 1;
        transform: scale(1);
    }
}

@keyframes pulse-ring {
    0% {
        opacity: 0.6;
        transform: scale(1);
    }

    100% {
        opacity: 0;
        transform: scale(2.8);
    }
}

@keyframes sym-float {
    0%,
    100% {
        transform: translateY(0);
        opacity: 0.5;
    }

    50% {
        transform: translateY(-4px);
        opacity: 0.85;
    }
}

@keyframes hex-pulse {
    0%,
    100% {
        stroke: rgba(199, 255, 73, 0.25);
    }

    50% {
        stroke: rgba(199, 255, 73, 0.5);
    }
}

@keyframes tech-in {
    from {
        opacity: 0;
        transform: scale(0.95) translateX(10px);
    }

    to {
        opacity: 1;
        transform: scale(1) translateX(0);
    }
}

@media (max-width: 900px) {
    .hero--home {
        grid-template-columns: 1fr;
    }

    .tech-visual {
        max-width: 360px;
        justify-self: center;
    }
}

@media (max-width: 680px) {
    .hero h1 {
        font-size: clamp(1.5rem, 8vw, 2.5rem);
    }

.hero--home h1 {
        font-size: clamp(2.5rem, 12vw, 4.75rem);
    }

    .hero__intro {
        grid-template-columns: 1fr;
        gap: 0.8rem;
    }

    .hero__cta {
        width: max-content;
    }

    .tech-visual {
        display: none;
    }
}
</style>
