<script setup>
import { computed } from 'vue';

const props = defineProps({
    category: {
        type: String,
        required: true,
    },
});

const content = {
    landing: {
        index: '01',
        kicker: 'Design & desenvolvimento',
        title: ['Páginas que', 'fazem acontecer.'],
        description: 'Landing pages rápidas, autorais e construídas para transformar atenção em resultado.',
        result: 'Clareza + conversão',
        code: ['narrativa precisa', 'interface responsiva', 'performance real'],
    },
    systems: {
        index: '02',
        kicker: 'Produto & arquitetura',
        title: ['Complexidade,', 'sem complicação.'],
        description: 'Sistemas web consistentes para organizar processos, dados e decisões do dia a dia.',
        result: 'Fluxo + escala',
        code: ['regras bem definidas', 'dados organizados', 'uso intuitivo'],
    },
    apps: {
        index: '03',
        kicker: 'Mobile & experiência',
        title: ['Ideias que cabem', 'na palma da mão.'],
        description: 'Aplicativos leves e diretos, desenhados para serem úteis desde o primeiro toque.',
        result: 'Utilidade + fluidez',
        code: ['jornada objetiva', 'interação natural', 'entrega multiplataforma'],
    },
};

const current = computed(() => content[props.category] ?? content.landing);
</script>

<template>
    <section class="hero" aria-live="polite">
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
                    <p>{{ current.description }}</p>
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

        <Transition name="object" mode="out-in">
            <aside :key="category" class="hero-object" aria-label="Resumo da categoria selecionada">
                <div class="hero-object__head">
                    <span>Campo selecionado</span>
                    <span>{{ current.index }} / 03</span>
                </div>

                <div class="hero-object__visual" aria-hidden="true">
                    <span class="orbit orbit--outer"></span>
                    <span class="orbit orbit--inner"></span>
                    <span class="scanner"></span>
                    <span class="axis axis--horizontal"></span>
                    <span class="axis axis--vertical"></span>
                    <span class="core">GL</span>
                </div>

                <div class="hero-object__foot">
                    <div>
                        <span>Resultado</span>
                        <strong>{{ current.result }}</strong>
                    </div>
                    <ol>
                        <li v-for="item in current.code" :key="item">{{ item }}</li>
                    </ol>
                </div>
            </aside>
        </Transition>
    </section>
</template>

<style lang="scss">
.hero {
    position: relative;
    min-height: 0;
    display: grid;
    grid-template-columns: minmax(0, 1.35fr) minmax(290px, 0.65fr);
    align-items: center;
    gap: clamp(2rem, 7vw, 8rem);
    padding: clamp(1.5rem, 4vh, 3.75rem) 0;
}

.hero__copy {
    min-width: 0;
}

.hero__kicker {
    margin: 0 0 clamp(1.1rem, 2.3vh, 2rem);
    color: var(--muted);
    font: 400 clamp(0.62rem, 0.75vw, 0.78rem)/1 'kodemono', monospace;
    letter-spacing: 0.12em;
    text-transform: uppercase;
}

.hero__kicker span {
    margin-right: 0.75rem;
    color: var(--accent);
}

.hero h1 {
    max-width: 960px;
    margin: 0;
    color: var(--ink);
    font: 400 clamp(2.65rem, 6.5vw, 7.1rem)/0.89 'open-sans', sans-serif;
    letter-spacing: -0.075em;
}

.hero h1 > span {
    display: block;
}

.hero h1 > span:last-child {
    color: transparent;
    -webkit-text-stroke: 1px rgba(238, 241, 232, 0.55);
}

.hero__intro {
    max-width: 690px;
    margin-top: clamp(1.25rem, 3.5vh, 3rem);
    padding-top: clamp(1rem, 2vh, 1.5rem);
    display: grid;
    grid-template-columns: 1fr auto;
    align-items: end;
    gap: 2rem;
    border-top: 1px solid var(--line);
}

.hero__intro p {
    max-width: 500px;
    margin: 0;
    color: var(--muted-light);
    font: 400 clamp(0.76rem, 0.95vw, 0.94rem)/1.7 'kodemono', monospace;
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

.hero-object {
    width: min(100%, 380px);
    justify-self: end;
    border: 1px solid var(--line);
    background: rgba(11, 13, 14, 0.58);
    box-shadow: 0 30px 80px rgba(0, 0, 0, 0.22);
    backdrop-filter: blur(18px);
}

.hero-object__head,
.hero-object__foot {
    padding: 0.9rem 1rem;
    display: flex;
    justify-content: space-between;
    gap: 1rem;
    color: var(--muted);
    font: 400 0.57rem/1 'kodemono', monospace;
    letter-spacing: 0.1em;
    text-transform: uppercase;
}

.hero-object__head {
    border-bottom: 1px solid var(--line);
}

.hero-object__head span:last-child {
    color: var(--accent);
}

.hero-object__visual {
    position: relative;
    min-height: clamp(175px, 30vh, 320px);
    overflow: hidden;
    background-image: linear-gradient(var(--line) 1px, transparent 1px), linear-gradient(90deg, var(--line) 1px, transparent 1px);
    background-size: 28px 28px;
    mask-image: linear-gradient(to bottom, transparent, #000 14%, #000 86%, transparent);
}

.orbit,
.core,
.axis,
.scanner {
    position: absolute;
    top: 50%;
    left: 50%;
}

.orbit {
    border: 1px solid rgba(199, 255, 73, 0.35);
    border-radius: 50%;
    transform: translate(-50%, -50%);
}

.orbit::before,
.orbit::after {
    content: '';
    position: absolute;
    width: 5px;
    aspect-ratio: 1;
    border-radius: 50%;
    background: var(--accent);
    box-shadow: 0 0 14px var(--accent);
}

.orbit--outer {
    width: min(74%, 250px);
    aspect-ratio: 1;
    animation: orbit-spin 14s linear infinite;
}

.orbit--outer::before {
    top: 17%;
    right: 10%;
}

.orbit--outer::after {
    bottom: 6%;
    left: 27%;
}

.orbit--inner {
    width: min(43%, 145px);
    aspect-ratio: 1;
    border-style: dashed;
    animation: orbit-spin-reverse 9s linear infinite;
}

.orbit--inner::before {
    top: -3px;
    left: 50%;
}

.orbit--inner::after {
    display: none;
}

.axis {
    background: rgba(238, 241, 232, 0.08);
    transform: translate(-50%, -50%);
}

.axis--horizontal {
    width: 82%;
    height: 1px;
}

.axis--vertical {
    width: 1px;
    height: 82%;
}

.scanner {
    width: min(74%, 250px);
    aspect-ratio: 1;
    border-radius: 50%;
    background: conic-gradient(from 10deg, rgba(199, 255, 73, 0.22), transparent 18%, transparent 100%);
    transform: translate(-50%, -50%);
    animation: scanner-spin 4.5s linear infinite;
}

.core {
    width: 3.3rem;
    aspect-ratio: 1;
    display: grid;
    place-items: center;
    border-radius: 50%;
    color: var(--bg);
    background: var(--accent);
    font: 600 0.7rem/1 'kodemono', monospace;
    letter-spacing: 0.08em;
    transform: translate(-50%, -50%);
    box-shadow: 0 0 0 7px rgba(199, 255, 73, 0.07), 0 0 40px rgba(199, 255, 73, 0.22);
}

.hero-object__foot {
    align-items: flex-end;
    border-top: 1px solid var(--line);
}

.hero-object__foot div {
    display: grid;
    gap: 0.45rem;
}

.hero-object__foot strong {
    color: var(--ink);
    font-size: 0.67rem;
    font-weight: 400;
    letter-spacing: 0;
    text-transform: none;
}

.hero-object__foot ol {
    margin: 0;
    padding: 0;
    display: grid;
    gap: 0.35rem;
    list-style: none;
    counter-reset: details;
    text-align: right;
    text-transform: none;
    letter-spacing: 0;
}

.hero-object__foot li {
    counter-increment: details;
}

.hero-object__foot li::before {
    content: '0' counter(details) ' ';
    color: var(--accent);
}

.category-enter-active,
.category-leave-active,
.object-enter-active,
.object-leave-active {
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

.object-enter-from {
    opacity: 0;
    transform: scale(0.96) rotate(1.5deg);
}

.object-leave-to {
    opacity: 0;
    transform: scale(1.02) rotate(-1deg);
}

@keyframes orbit-spin {
    to { transform: translate(-50%, -50%) rotate(360deg); }
}

@keyframes orbit-spin-reverse {
    to { transform: translate(-50%, -50%) rotate(-360deg); }
}

@keyframes scanner-spin {
    to { transform: translate(-50%, -50%) rotate(360deg); }
}

@media (max-width: 900px) {
    .hero {
        grid-template-columns: minmax(0, 1fr) minmax(220px, 0.42fr);
        gap: 1.5rem;
        padding: 1.5rem 0;
    }

    .hero h1 {
        font-size: clamp(2.65rem, 8.2vw, 5rem);
    }

    .hero-object__foot ol {
        display: none;
    }
}

@media (max-width: 680px) {
    .hero {
        grid-template-columns: 1fr;
        align-content: center;
        padding: 1.25rem 0;
    }

    .hero h1 {
        font-size: clamp(2.5rem, 12vw, 4.75rem);
    }

    .hero__intro {
        margin-top: 1.2rem;
        grid-template-columns: 1fr;
        gap: 0.8rem;
    }

    .hero__intro a {
        width: max-content;
    }

    .hero-object {
        display: none;
    }
}

@media (max-height: 700px) {
    .hero__kicker {
        margin-bottom: 0.8rem;
    }

    .hero__intro {
        margin-top: 1rem;
        padding-top: 0.8rem;
    }

    .hero-object__visual {
        min-height: 165px;
    }
}
</style>
