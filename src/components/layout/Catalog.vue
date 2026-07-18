<script setup>
import { computed, ref } from 'vue';

const props = defineProps({
    category: {
        type: String,
        required: true,
    },
});

const lightbox = ref({ open: false, src: '', title: '' });

function openLightbox(src, title) {
    lightbox.value = { open: true, src, title };
}

function closeLightbox() {
    lightbox.value.open = false;
}

const projects = {
    landing: [
        {
            id: 1,
            title: 'Magnus Assessment',
            description: 'Plataforma de avaliação comportamental com relatórios analíticos completos.',
            tags: ['Vue.js', 'Laravel', 'Charts'],
            status: 'Concluído',
            image: '/projects/landing-magnus.png',
        },
        {
            id: 2,
            title: 'Modelify',
            description: 'Landing page para SaaS de modelagem de dados com CTA e formulário integrado.',
            tags: ['Nuxt', 'Tailwind', 'SEO'],
            status: 'Concluído',
            image: '/projects/landing-modelify.png',
        },
        {
            id: 3,
            title: 'Studio Revive',
            description: 'Página institucional para estúdio de design com animações scroll-driven.',
            tags: ['HTML', 'CSS', 'GSAP'],
            status: 'Concluído',
            image: '/projects/landing-studio.png',
        },
    ],
    systems: [
        {
            id: 1,
            title: 'ERP Interno',
            description: 'Sistema de gestão de processos internos com controle de fluxo e permissões.',
            tags: ['Laravel', 'Vue.js', 'MySQL'],
            status: 'Em produção',
            image: '/projects/system-erp.png',
        },
        {
            id: 2,
            title: 'Painel Administrativo',
            description: 'Dashboard para gerenciamento de usuários, relatórios e métricas em tempo real.',
            tags: ['Vue.js', 'REST API', 'Charts'],
            status: 'Em produção',
            image: '/projects/system-admin.png',
        },
        {
            id: 3,
            title: 'CRM de Vendas',
            description: 'Pipeline de vendas com automações, notificações e integrações com WhatsApp.',
            tags: ['Laravel', 'Livewire', 'Redis'],
            status: 'Concluído',
            image: '/projects/system-crm.png',
        },
    ],
    apps: [
        {
            id: 1,
            title: 'App de Delivery',
            description: 'Aplicativo de entregas com rastreamento em tempo real e notificações push.',
            tags: ['Flutter', 'Firebase', 'Maps'],
            status: 'Concluído',
            image: '/projects/app-delivery.png',
        },
        {
            id: 2,
            title: 'Controle Financeiro',
            description: 'App pessoal de finanças com gráficos, metas e categorização automática.',
            tags: ['Flutter', 'SQLite', 'Charts'],
            status: 'Em desenvolvimento',
            image: '/projects/app-finance.png',
        },
        {
            id: 3,
            title: 'App Institucional',
            description: 'Aplicativo vitrine com catálogo de serviços, agendamento e chat integrado.',
            tags: ['Flutter', 'Laravel API', 'Push'],
            status: 'Concluído',
            image: '/projects/app-institutional.png',
        },
    ],
};

const items = computed(() => projects[props.category] ?? []);
const showCatalog = computed(() => ['landing', 'systems', 'apps'].includes(props.category));
</script>

<template>
    <Transition name="catalog">
        <section v-if="showCatalog" class="catalog" aria-label="Catálogo de projetos">
            <div class="catalog__header">
                <span class="catalog__label">Projetos</span>
                <span class="catalog__count">{{ items.length }} itens</span>
            </div>

            <TransitionGroup name="card" tag="div" class="catalog__grid">
                <article
                    v-for="(project, index) in items"
                    :key="`${category}-${project.id}`"
                    class="project-card"
                    :style="{ '--delay': `${index * 80}ms` }"
                >
                    <button
                        class="project-card__image"
                        type="button"
                        @click="openLightbox(project.image, project.title)"
                        :aria-label="`Ver imagem de ${project.title}`"
                    >
                        <img :src="project.image" :alt="project.title" loading="lazy" />
                        <span class="project-card__zoom" aria-hidden="true">
                            <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                                <circle cx="11" cy="11" r="8"/><line x1="21" y1="21" x2="16.65" y2="16.65"/><line x1="11" y1="8" x2="11" y2="14"/><line x1="8" y1="11" x2="14" y2="11"/>
                            </svg>
                        </span>
                    </button>

                    <div class="project-card__info">
                        <div class="project-card__head">
                            <span class="project-card__number">{{ String(project.id).padStart(2, '0') }}</span>
                            <span class="project-card__status" :class="{ 'is-active': project.status !== 'Concluído' }">
                                {{ project.status }}
                            </span>
                        </div>

                        <div class="project-card__body">
                            <h3>{{ project.title }}</h3>
                            <p>{{ project.description }}</p>
                        </div>

                        <div class="project-card__tags">
                            <span v-for="tag in project.tags" :key="tag">{{ tag }}</span>
                        </div>
                    </div>

                    <div class="project-card__glow" aria-hidden="true"></div>
                </article>
            </TransitionGroup>
        </section>
    </Transition>

    <!-- Lightbox -->
    <Teleport to="body">
        <Transition name="lightbox">
            <div
                v-if="lightbox.open"
                class="lightbox"
                @click.self="closeLightbox"
                role="dialog"
                aria-modal="true"
                :aria-label="`Imagem: ${lightbox.title}`"
            >
                <button class="lightbox__close" @click="closeLightbox" aria-label="Fechar lightbox">
                    <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                        <line x1="18" y1="6" x2="6" y2="18"/><line x1="6" y1="6" x2="18" y2="18"/>
                    </svg>
                </button>
                <div class="lightbox__content">
                    <img :src="lightbox.src" :alt="lightbox.title" />
                    <p class="lightbox__caption">{{ lightbox.title }}</p>
                </div>
            </div>
        </Transition>
    </Teleport>
</template>

<style lang="scss">
.catalog {
    padding-top: clamp(0.5rem, 1.5vh, 1.25rem);
    padding-bottom: 1.5rem;
    overflow-y: auto;
    scrollbar-width: thin;
    scrollbar-color: rgba(199, 255, 73, 0.2) transparent;
}

.catalog__header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: clamp(0.8rem, 1.5vh, 1.25rem);
    padding-bottom: 0.6rem;
    border-bottom: 1px solid var(--line);
}

.catalog__label {
    color: var(--muted);
    font: 400 0.55rem/1 'kodemono', monospace;
    letter-spacing: 0.13em;
    text-transform: uppercase;
}

.catalog__count {
    color: var(--accent);
    font: 400 0.55rem/1 'kodemono', monospace;
    letter-spacing: 0.08em;
}

.catalog__grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: clamp(0.7rem, 1.2vw, 1rem);
}

/* Card */
.project-card {
    position: relative;
    display: flex;
    flex-direction: column;
    border: 1px solid var(--line);
    background: rgba(11, 13, 14, 0.5);
    backdrop-filter: blur(12px);
    overflow: hidden;
    transition: border-color 320ms ease, box-shadow 320ms ease;
    animation: card-in 500ms var(--ease-out) both;
    animation-delay: var(--delay);
}

.project-card:hover {
    border-color: rgba(199, 255, 73, 0.2);
    box-shadow: 0 8px 40px rgba(0, 0, 0, 0.25);
}

.project-card:hover .project-card__glow {
    opacity: 1;
}

.project-card__glow {
    position: absolute;
    inset: 0;
    opacity: 0;
    background: radial-gradient(circle at 30% 20%, rgba(199, 255, 73, 0.06), transparent 60%);
    pointer-events: none;
    transition: opacity 400ms ease;
}

/* Image */
.project-card__image {
    position: relative;
    display: block;
    width: 100%;
    aspect-ratio: 16 / 10;
    padding: 0;
    border: 0;
    border-bottom: 1px solid var(--line);
    background: rgba(0, 0, 0, 0.3);
    cursor: pointer;
    overflow: hidden;
}

.project-card__image img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    transition: transform 400ms var(--ease-out), filter 400ms ease;
}

.project-card:hover .project-card__image img {
    transform: scale(1.04);
    filter: brightness(1.1);
}

.project-card__zoom {
    position: absolute;
    inset: 0;
    display: grid;
    place-items: center;
    background: rgba(0, 0, 0, 0.5);
    color: var(--accent);
    opacity: 0;
    transition: opacity 260ms ease;
}

.project-card__image:hover .project-card__zoom {
    opacity: 1;
}

/* Info */
.project-card__info {
    position: relative;
    z-index: 1;
    display: flex;
    flex-direction: column;
    gap: 0.6rem;
    padding: clamp(0.7rem, 1.2vw, 1rem);
}

.project-card__head {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.project-card__number {
    color: var(--accent);
    font: 500 0.6rem/1 'kodemono', monospace;
    letter-spacing: 0.1em;
}

.project-card__status {
    padding: 0.2rem 0.5rem;
    border: 1px solid var(--line);
    color: var(--muted);
    font: 400 0.5rem/1 'kodemono', monospace;
    letter-spacing: 0.06em;
    text-transform: uppercase;
}

.project-card__status.is-active {
    border-color: rgba(199, 255, 73, 0.25);
    color: var(--accent);
}

.project-card__body {
    flex: 1;
    display: flex;
    flex-direction: column;
    gap: 0.3rem;
}

.project-card__body h3 {
    margin: 0;
    color: var(--ink);
    font: 400 clamp(0.78rem, 0.95vw, 0.9rem)/1.2 'open-sans', sans-serif;
    letter-spacing: -0.02em;
}

.project-card__body p {
    margin: 0;
    color: var(--muted-light);
    font: 400 0.6rem/1.55 'kodemono', monospace;
}

.project-card__tags {
    display: flex;
    flex-wrap: wrap;
    gap: 0.3rem;
}

.project-card__tags span {
    padding: 0.15rem 0.4rem;
    border: 1px solid var(--line);
    color: var(--muted);
    font: 400 0.46rem/1 'kodemono', monospace;
    letter-spacing: 0.05em;
    text-transform: uppercase;
    transition: color 200ms ease, border-color 200ms ease;
}

.project-card:hover .project-card__tags span {
    border-color: rgba(199, 255, 73, 0.15);
    color: var(--muted-light);
}

/* Lightbox */
.lightbox {
    position: fixed;
    z-index: 9999;
    inset: 0;
    display: grid;
    place-items: center;
    padding: 2rem;
    background: rgba(0, 0, 0, 0.88);
    backdrop-filter: blur(20px);
    cursor: pointer;
}

.lightbox__close {
    position: absolute;
    top: 1.5rem;
    right: 1.5rem;
    z-index: 2;
    width: 2.5rem;
    height: 2.5rem;
    display: grid;
    place-items: center;
    padding: 0;
    border: 1px solid var(--line-strong);
    border-radius: 50%;
    background: rgba(9, 11, 12, 0.7);
    color: var(--ink);
    cursor: pointer;
    transition: border-color 200ms ease, color 200ms ease;
}

.lightbox__close:hover {
    border-color: var(--accent);
    color: var(--accent);
}

.lightbox__content {
    max-width: min(90vw, 1100px);
    max-height: 85vh;
    display: flex;
    flex-direction: column;
    gap: 0.8rem;
    cursor: default;
}

.lightbox__content img {
    width: 100%;
    max-height: 80vh;
    object-fit: contain;
    border: 1px solid var(--line);
    box-shadow: 0 30px 100px rgba(0, 0, 0, 0.5);
}

.lightbox__caption {
    margin: 0;
    text-align: center;
    color: var(--muted-light);
    font: 400 0.65rem/1 'kodemono', monospace;
    letter-spacing: 0.08em;
    text-transform: uppercase;
}

/* Lightbox transitions */
.lightbox-enter-active,
.lightbox-leave-active {
    transition: opacity 280ms ease;
}

.lightbox-enter-active .lightbox__content,
.lightbox-leave-active .lightbox__content {
    transition: transform 350ms var(--ease-out), opacity 280ms ease;
}

.lightbox-enter-from {
    opacity: 0;
}

.lightbox-enter-from .lightbox__content {
    opacity: 0;
    transform: scale(0.92);
}

.lightbox-leave-to {
    opacity: 0;
}

.lightbox-leave-to .lightbox__content {
    opacity: 0;
    transform: scale(1.03);
}

/* Card transitions */
.catalog-enter-active,
.catalog-leave-active {
    transition: opacity 300ms ease, transform 400ms var(--ease-out);
}

.catalog-enter-from {
    opacity: 0;
    transform: translateY(12px);
}

.catalog-leave-to {
    opacity: 0;
    transform: translateY(-8px);
}

.card-enter-active {
    transition: opacity 400ms ease, transform 400ms var(--ease-out);
    transition-delay: var(--delay);
}

.card-leave-active {
    transition: opacity 200ms ease, transform 200ms ease;
}

.card-enter-from {
    opacity: 0;
    transform: translateY(16px) scale(0.97);
}

.card-leave-to {
    opacity: 0;
    transform: scale(0.96);
}

@keyframes card-in {
    from {
        opacity: 0;
        transform: translateY(14px);
    }
    to {
        opacity: 1;
        transform: translateY(0);
    }
}

@media (max-width: 900px) {
    .catalog__grid {
        grid-template-columns: repeat(2, 1fr);
    }
}

@media (max-width: 580px) {
    .catalog__grid {
        grid-template-columns: 1fr;
    }

    .lightbox {
        padding: 1rem;
    }
}
</style>
