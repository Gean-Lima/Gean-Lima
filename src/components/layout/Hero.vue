<script setup>
import { computed } from 'vue';

const props = defineProps({
    category: {
        type: String,
        required: true,
    },
});

const content = {
    home: {
        index: '01',
        kicker: 'Desenvolvedor Full-stack',
        title: ['Gean Lima'],
        description: 'Desenvolvedor focado em criar aplicações web e mobile consistentes, unindo design intuitivo e arquitetura robusta.',
    },
    landing: {
        index: '02',
        kicker: 'Design & desenvolvimento',
        title: ['Páginas que', 'fazem acontecer.'],
        description: 'Landing pages rápidas, autorais e construídas para transformar atenção em resultado.',
    },
    systems: {
        index: '03',
        kicker: 'Produto & arquitetura',
        title: ['Complexidade,', 'sem complicação.'],
        description: 'Sistemas web consistentes para organizar processos, dados e decisões do dia a dia.',
    },
    apps: {
        index: '04',
        kicker: 'Mobile & experiência',
        title: ['Ideias que cabem', 'na palma da mão.'],
        description: 'Aplicativos leves e diretos, desenhados para serem úteis desde o primeiro toque.',
    },
};

const current = computed(() => content[props.category] ?? content.home);
const isHome = computed(() => props.category === 'home');
</script>

<template>
    <section class="hero" :class="{ 'hero--home': isHome }" aria-live="polite">
        <Transition name="category" mode="out-in">
            <div :key="category" class="hero__copy">
                <p class="hero__kicker">
                    <span>{{ current.index }}</span>
                    {{ current.kicker }}
                </p>

                <h1>
                    <span v-for="line in current.title" :key="line">{{ line }}</span>
                </h1>

                <div class="hero__intro">
                    <div class="hero__intro-text">
                        <p>{{ current.description }}</p>
                        <div v-if="isHome" class="hero__simple-details">
                            <p><strong>Experiência:</strong> 2018—Agora · Desenvolvimento full-stack</p>
                            <p><strong>Stack:</strong> Laravel · Vue.js · Nuxt · Flutter · PHP · MySQL</p>
                        </div>
                    </div>
                    <a
                        href="https://www.linkedin.com/in/gean-lima-775b491a2/"
                        target="_blank"
                        rel="noopener noreferrer"
                    >
                        Iniciar um projeto
                        <span aria-hidden="true">↗</span>
                    </a>
                </div>
            </div>
        </Transition>

        <!-- Tech SVG animation for home -->
        <Transition name="tech-visual" mode="out-in">
            <div v-if="isHome" class="tech-visual" aria-hidden="true">
                <svg viewBox="0 0 480 320" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <!-- Grid -->
                    <defs>
                        <pattern id="grid" width="40" height="40" patternUnits="userSpaceOnUse">
                            <path d="M 40 0 L 0 0 0 40" fill="none" stroke="rgba(238,241,232,0.04)" stroke-width="0.5"/>
                        </pattern>
                        <radialGradient id="fade" cx="50%" cy="50%" r="50%">
                            <stop offset="0%" stop-color="white"/>
                            <stop offset="100%" stop-color="white" stop-opacity="0"/>
                        </radialGradient>
                        <mask id="fade-mask">
                            <rect width="480" height="320" fill="url(#fade)"/>
                        </mask>
                    </defs>

                    <rect width="480" height="320" fill="url(#grid)" mask="url(#fade-mask)"/>

                    <!-- Circuit lines -->
                    <g class="circuit-lines" stroke="rgba(199,255,73,0.12)" stroke-width="1" fill="none">
                        <polyline points="60,160 120,160 140,120 200,120 220,160 280,160" class="circuit-path circuit-path--1"/>
                        <polyline points="200,200 260,200 280,160 340,160 360,200 420,200" class="circuit-path circuit-path--2"/>
                        <polyline points="120,80 160,80 180,120 200,120" class="circuit-path circuit-path--3"/>
                        <polyline points="280,160 300,120 360,120 380,80" class="circuit-path circuit-path--4"/>
                        <polyline points="160,240 200,240 220,200 260,200" class="circuit-path circuit-path--5"/>
                        <polyline points="340,160 360,200 380,240 420,240" class="circuit-path circuit-path--6"/>
                    </g>

                    <!-- Nodes -->
                    <g class="nodes">
                        <circle cx="120" cy="160" r="3" fill="rgba(199,255,73,0.5)" class="node node--1"/>
                        <circle cx="200" cy="120" r="3" fill="rgba(199,255,73,0.5)" class="node node--2"/>
                        <circle cx="280" cy="160" r="4" fill="rgba(199,255,73,0.7)" class="node node--3"/>
                        <circle cx="340" cy="160" r="3" fill="rgba(199,255,73,0.5)" class="node node--4"/>
                        <circle cx="200" cy="200" r="3" fill="rgba(199,255,73,0.4)" class="node node--5"/>
                        <circle cx="360" cy="200" r="3" fill="rgba(199,255,73,0.4)" class="node node--6"/>
                        <circle cx="120" cy="80" r="2.5" fill="rgba(199,255,73,0.3)" class="node node--7"/>
                        <circle cx="380" cy="80" r="2.5" fill="rgba(199,255,73,0.3)" class="node node--8"/>
                        <circle cx="160" cy="240" r="2.5" fill="rgba(199,255,73,0.3)" class="node node--9"/>
                        <circle cx="420" cy="240" r="2.5" fill="rgba(199,255,73,0.3)" class="node node--10"/>
                    </g>

                    <!-- Pulse rings -->
                    <circle cx="280" cy="160" r="8" fill="none" stroke="rgba(199,255,73,0.2)" stroke-width="0.5" class="pulse pulse--1"/>
                    <circle cx="280" cy="160" r="16" fill="none" stroke="rgba(199,255,73,0.1)" stroke-width="0.5" class="pulse pulse--2"/>
                    <circle cx="280" cy="160" r="26" fill="none" stroke="rgba(199,255,73,0.05)" stroke-width="0.5" class="pulse pulse--3"/>

                    <!-- Data packets moving along paths -->
                    <circle r="2" fill="var(--accent)" class="packet packet--1">
                        <animateMotion dur="3.5s" repeatCount="indefinite" path="M60,160 L120,160 L140,120 L200,120 L220,160 L280,160"/>
                    </circle>
                    <circle r="2" fill="var(--accent)" class="packet packet--2">
                        <animateMotion dur="4s" repeatCount="indefinite" path="M200,200 L260,200 L280,160 L340,160 L360,200 L420,200" begin="1.5s"/>
                    </circle>
                    <circle r="1.5" fill="var(--accent)" class="packet packet--3">
                        <animateMotion dur="2.5s" repeatCount="indefinite" path="M120,80 L160,80 L180,120 L200,120" begin="0.8s"/>
                    </circle>

                    <!-- Floating brackets / code symbols -->
                    <text x="80" y="100" fill="rgba(199,255,73,0.12)" font-family="'kodemono', monospace" font-size="11" class="code-sym code-sym--1">&lt;/&gt;</text>
                    <text x="350" y="100" fill="rgba(199,255,73,0.1)" font-family="'kodemono', monospace" font-size="10" class="code-sym code-sym--2">{ }</text>
                    <text x="100" y="260" fill="rgba(199,255,73,0.08)" font-family="'kodemono', monospace" font-size="9" class="code-sym code-sym--3">fn()</text>
                    <text x="380" y="270" fill="rgba(199,255,73,0.1)" font-family="'kodemono', monospace" font-size="10" class="code-sym code-sym--4">[ ]</text>
                    <text x="220" y="70" fill="rgba(199,255,73,0.07)" font-family="'kodemono', monospace" font-size="8" class="code-sym code-sym--5">0x1F</text>
                    <text x="300" y="270" fill="rgba(199,255,73,0.07)" font-family="'kodemono', monospace" font-size="8" class="code-sym code-sym--6">async</text>

                    <!-- Central hexagon -->
                    <polygon points="280,138 296,149 296,171 280,182 264,171 264,149" fill="none" stroke="rgba(199,255,73,0.25)" stroke-width="0.8" class="hex"/>
                    <text x="280" y="164" text-anchor="middle" fill="rgba(199,255,73,0.6)" font-family="'kodemono', monospace" font-size="8" font-weight="600" class="hex-label">GL</text>
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
    padding: clamp(1.5rem, 4vh, 3.75rem) 0;
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
    margin-bottom: clamp(1.1rem, 2.3vh, 2rem);
}

.hero__kicker span {
    margin-right: 0.75rem;
    color: var(--accent);
}

.hero h1 {
    max-width: 960px;
    margin: 0;
    color: var(--ink);
    font: 400 clamp(1.6rem, 3.5vw, 3.5rem)/0.92 'open-sans', sans-serif;
    letter-spacing: -0.06em;
}

.hero--home h1 {
    font-size: clamp(2.65rem, 6.5vw, 7.1rem);
    line-height: 0.89;
    letter-spacing: -0.075em;
}

.hero h1 > span {
    display: block;
}

.hero h1 > span:last-child {
    color: transparent;
    -webkit-text-stroke: 1px rgba(238, 241, 232, 0.55);
}

.hero--home h1 > span:only-child {
    color: var(--ink);
    -webkit-text-stroke: 0;
}

.hero__intro {
    margin-top: clamp(0.6rem, 1.5vh, 1rem);
    padding-top: clamp(0.5rem, 1vh, 0.75rem);
    display: grid;
    grid-template-columns: 1fr auto;
    align-items: end;
    gap: 2rem;
    border-top: 1px solid var(--line);
}

.hero--home .hero__intro {
    margin-top: clamp(1.25rem, 3.5vh, 3rem);
    padding-top: clamp(1rem, 2vh, 1.5rem);
}

.hero__intro p {
    max-width: 500px;
    margin: 0;
    color: var(--muted-light);
    font: 400 clamp(0.68rem, 0.85vw, 0.82rem)/1.7 'kodemono', monospace;
}

.hero--home .hero__intro p {
    font-size: clamp(0.76rem, 0.95vw, 0.94rem);
}

.hero__simple-details {
    margin-top: 1.2rem;
    display: flex;
    flex-direction: column;
    gap: 0.4rem;
}

.hero__simple-details p {
    font-size: 0.72rem;
    color: var(--muted);
}

.hero__simple-details strong {
    color: var(--accent);
    font-weight: 500;
}

.hero__intro a {
    padding-bottom: 0.3rem;
    color: var(--ink);
    border-bottom: 1px solid var(--accent);
    font: 500 0.7rem/1 'kodemono', monospace;
    letter-spacing: 0.05em;
    text-decoration: none;
    white-space: nowrap;
}

.hero__intro a span {
    display: inline-block;
    margin-left: 0.5rem;
    color: var(--accent);
    transition: transform 200ms ease;
}

.hero__intro a:hover span {
    transform: translate(3px, -3px);
}

/* Tech Visual */
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

/* Circuit path drawing */
.circuit-path {
    stroke-dasharray: 400;
    stroke-dashoffset: 400;
    animation: draw-line 2s var(--ease-out) forwards;
}

.circuit-path--1 { animation-delay: 0.2s; }
.circuit-path--2 { animation-delay: 0.5s; }
.circuit-path--3 { animation-delay: 0.7s; }
.circuit-path--4 { animation-delay: 0.9s; }
.circuit-path--5 { animation-delay: 1.1s; }
.circuit-path--6 { animation-delay: 1.3s; }

/* Nodes */
.node {
    opacity: 0;
    animation: node-pop 400ms var(--ease-out) forwards;
}
.node--1 { animation-delay: 0.6s; }
.node--2 { animation-delay: 0.8s; }
.node--3 { animation-delay: 1.0s; }
.node--4 { animation-delay: 1.1s; }
.node--5 { animation-delay: 1.2s; }
.node--6 { animation-delay: 1.3s; }
.node--7 { animation-delay: 1.4s; }
.node--8 { animation-delay: 1.5s; }
.node--9 { animation-delay: 1.6s; }
.node--10 { animation-delay: 1.7s; }

/* Pulse rings */
.pulse {
    animation: pulse-ring 3s ease-out infinite;
}
.pulse--2 { animation-delay: 0.6s; }
.pulse--3 { animation-delay: 1.2s; }

/* Data packets glow */
.packet {
    filter: drop-shadow(0 0 4px rgba(199,255,73,0.6));
}

/* Code symbols float */
.code-sym {
    animation: sym-float 6s ease-in-out infinite;
}
.code-sym--1 { animation-delay: 0s; }
.code-sym--2 { animation-delay: 1s; }
.code-sym--3 { animation-delay: 2s; }
.code-sym--4 { animation-delay: 3s; }
.code-sym--5 { animation-delay: 1.5s; }
.code-sym--6 { animation-delay: 4s; }

/* Hexagon */
.hex {
    animation: hex-pulse 4s ease-in-out infinite;
}

@keyframes draw-line {
    to { stroke-dashoffset: 0; }
}

@keyframes node-pop {
    from { opacity: 0; transform: scale(0); }
    to { opacity: 1; transform: scale(1); }
}

@keyframes pulse-ring {
    0% { opacity: 0.6; transform: scale(1); }
    100% { opacity: 0; transform: scale(2.8); }
}

@keyframes sym-float {
    0%, 100% { transform: translateY(0); opacity: 1; }
    50% { transform: translateY(-6px); opacity: 0.6; }
}

@keyframes hex-pulse {
    0%, 100% { stroke: rgba(199,255,73,0.25); }
    50% { stroke: rgba(199,255,73,0.5); }
}

@keyframes tech-in {
    from { opacity: 0; transform: scale(0.95) translateX(20px); }
    to { opacity: 1; transform: scale(1) translateX(0); }
}

/* Transitions */
.category-enter-active,
.category-leave-active {
    transition: opacity 320ms ease, transform 520ms var(--ease-out), filter 320ms ease;
}

.category-enter-from {
    opacity: 0;
    transform: translateY(18px);
    filter: blur(6px);
}

.category-leave-to {
    opacity: 0;
    transform: translateY(-12px);
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

    .hero__intro a {
        width: max-content;
    }

    .tech-visual {
        display: none;
    }
}
</style>
