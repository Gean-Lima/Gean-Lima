<script setup>
import { onBeforeUnmount, onMounted, ref } from 'vue';
import IconMark from '@/components/ui/IconMark.vue';

defineProps({
    modelValue: {
        type: String,
        required: true,
    },
});

const emit = defineEmits(['update:modelValue']);
const header = ref(null);
const isMenuOpen = ref(false);

const closeMenu = () => {
    isMenuOpen.value = false;
};

const selectCategory = (categoryId) => {
    emit('update:modelValue', categoryId);
    closeMenu();
};

const handleKeydown = (event) => {
    if (event.key === 'Escape') closeMenu();
};

const handlePointerDown = (event) => {
    if (isMenuOpen.value && !header.value?.contains(event.target)) closeMenu();
};

const handleResize = () => {
    if (window.innerWidth > 900) closeMenu();
};

onMounted(() => {
    document.addEventListener('keydown', handleKeydown);
    document.addEventListener('pointerdown', handlePointerDown);
    window.addEventListener('resize', handleResize);
});

onBeforeUnmount(() => {
    document.removeEventListener('keydown', handleKeydown);
    document.removeEventListener('pointerdown', handlePointerDown);
    window.removeEventListener('resize', handleResize);
});

const categories = [
    { id: 'home', label: 'Início' },
    { id: 'landing', label: 'Landing Pages' },
    { id: 'systems', label: 'Sistemas Web' },
    { id: 'apps', label: 'Apps' },
];

const socialLinks = [
    {
        id: 'github',
        label: 'GitHub',
        href: 'https://github.com/Gean-Lima',
        icon: 'github',
    },
    {
        id: 'linkedin',
        label: 'LinkedIn',
        href: 'https://www.linkedin.com/in/gean-lima-775b491a2/',
        icon: 'linkedin',
    }
];
</script>

<template>
    <header ref="header" class="site-header" :class="{ 'menu-is-open': isMenuOpen }">
        <nav
            id="portfolio-menu"
            class="category-nav"
            :class="{ 'is-open': isMenuOpen }"
            aria-label="Categorias do portfólio"
        >
            <button
                v-for="(category, index) in categories"
                :key="category.id"
                type="button"
                :class="{ 'is-active': modelValue === category.id }"
                :aria-pressed="modelValue === category.id"
                @click="selectCategory(category.id)"
            >
                {{ category.label }}
            </button>
        </nav>

        <div class="header-links" aria-label="Redes e contato">
            <button
                class="menu-toggle"
                type="button"
                aria-controls="portfolio-menu"
                :aria-expanded="isMenuOpen"
                :aria-label="isMenuOpen ? 'Fechar menu' : 'Abrir menu'"
                @click.stop="isMenuOpen = !isMenuOpen"
            >
                <span class="menu-toggle__label">{{ isMenuOpen ? 'Fechar' : 'Menu' }}</span>
                <span class="menu-toggle__icon" aria-hidden="true">
                    <i></i>
                    <i></i>
                </span>
            </button>

            <div class="header-links__actions">
                <template v-for="link in socialLinks" :key="link.id">
                    <a
                        v-if="!link.disabled"
                        class="header-links__icon-link"
                        :href="link.href"
                        target="_blank"
                        rel="noopener noreferrer"
                        :aria-label="link.label"
                        :title="link.label"
                    >
                        <IconMark :name="link.icon" />
                        <span class="sr-only">{{ link.label }}</span>
                    </a>
    
                    <button
                        v-else
                        class="header-links__icon-button"
                        type="button"
                        disabled
                        :aria-label="`${link.label} não configurado`"
                        :title="`${link.label} não configurado`"
                    >
                        <IconMark :name="link.icon" />
                        <span class="sr-only">{{ link.label }}</span>
                    </button>
                </template>

                <a
                    class="header-links__contact"
                    href="https://www.linkedin.com/in/gean-lima-775b491a2/"
                    target="_blank"
                    rel="noopener noreferrer"
                >
                    <span>Vamos conversar</span>
                    <IconMark name="whatsapp" />
                </a>
            </div>
        </div>
    </header>
</template>

<style lang="scss">
.site-header {
    position: relative;
    z-index: 20;
    width: min(100% - 6vw, 1440px);
    height: var(--header-height);
    margin: 0 auto;
    display: flex;
    align-items: center;
    justify-content: space-between;
    border-bottom: 1px solid var(--line);
    animation: header-in 800ms var(--ease-out) both;
}

.brand {
    width: max-content;
    display: inline-flex;
    align-items: center;
    gap: 0.7rem;
    color: var(--ink);
    text-decoration: none;
}

.brand__mark {
    width: 2rem;
    aspect-ratio: 1;
    display: grid;
    place-items: center;
    border: 1px solid var(--accent);
    border-radius: 50%;
    color: var(--accent);
    font: 500 0.8rem/1 'kodemono', monospace;
    box-shadow: inset 0 0 14px rgba(199, 255, 73, 0.08);
}

.brand__name {
    font: 500 0.76rem/1 'kodemono', monospace;
    letter-spacing: 0.13em;
    text-transform: uppercase;
}

.category-nav {
    height: 100%;
    display: flex;
    align-items: stretch;
    gap: clamp(1rem, 3vw, 3.5rem);
}

.category-nav button {
    position: relative;
    padding: 0;
    border: 0;
    background: transparent;
    color: var(--muted);
    font: 400 clamp(0.67rem, 0.72vw, 0.78rem)/1 'kodemono', monospace;
    letter-spacing: 0.06em;
    transition: color 220ms ease;
}

.category-nav button::after {
    content: '';
    position: absolute;
    right: 0;
    bottom: -1px;
    left: 0;
    height: 1px;
    background: var(--accent);
    transform: scaleX(0);
    transform-origin: right;
    transition: transform 420ms var(--ease-out);
}

.category-nav button:hover,
.category-nav button.is-active {
    color: var(--ink);
}

.category-nav button.is-active::after {
    transform: scaleX(1);
    transform-origin: left;
}

.category-nav__number {
    margin-right: 0.35rem;
    color: var(--accent);
    font-size: 0.55rem;
    vertical-align: top;
}

.header-links {
    display: flex;
    justify-content: flex-end;
    align-items: center;
    gap: 0.6rem;
}

.header-links__actions {
    display: flex;
    gap: 0.5rem;
}

.menu-toggle {
    display: none;
}

.header-links__icon-link,
.header-links__icon-button {
    width: 2.3rem;
    height: 2.3rem;
    display: grid;
    place-items: center;
    border: 1px solid var(--line);
    border-radius: 50%;
    background: rgba(11, 13, 14, 0.45);
    color: var(--muted);
    text-decoration: none;
    transition: color 200ms ease, border-color 200ms ease, transform 200ms ease, background 200ms ease;
}

.header-links__icon-link:hover,
.header-links__icon-button:hover {
    color: var(--accent);
    border-color: rgba(199, 255, 73, 0.28);
    background: rgba(199, 255, 73, 0.04);
    transform: translateY(-1px);
}

.header-links__icon-button {
    padding: 0;
}

.header-links__icon-button:disabled {
    opacity: 0.5;
    cursor: not-allowed;
    transform: none;
}

.header-links__icon-link svg,
.header-links__icon-button svg {
    width: 1rem;
    height: 1rem;
}

.header-links .header-links__contact {
    margin-left: 0.3rem;
    padding: 0.75rem 0.9rem;
    border: 1px solid var(--line-strong);
    color: var(--ink);
    display: inline-flex;
    align-items: center;
    gap: 0.5rem;
    text-decoration: none;
    font: 500 0.64rem/1 'kodemono', monospace;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    transition: border-color 200ms ease, color 200ms ease, background 200ms ease;
    background-color: transparent;
}

.header-links__contact:hover {
    border-color: rgba(199, 255, 73, 0.28);
    color: var(--accent);
    background: rgba(199, 255, 73, 0.03);
}

.header-links__contact svg {
    width: 0.95rem;
    height: 0.95rem;
}

.sr-only {
    position: absolute;
    width: 1px;
    height: 1px;
    padding: 0;
    margin: -1px;
    overflow: hidden;
    clip: rect(0, 0, 0, 0);
    white-space: nowrap;
    border: 0;
}

@media (max-width: 900px) {
    .site-header {
        width: min(100% - 2rem, 720px);
        height: clamp(4.5rem, 10vh, 5.5rem);
    }

    .menu-toggle {
        display: inline-flex;
        align-items: center;
        gap: 0.7rem;
        min-height: 2.5rem;
        padding: 0 0.85rem;
        border: 1px solid var(--line-strong);
        background: rgba(11, 13, 14, 0.72);
        color: var(--ink);
        font: 500 0.62rem/1 'kodemono', monospace;
        letter-spacing: 0.1em;
        text-transform: uppercase;
        transition: color 200ms ease, border-color 200ms ease, background 200ms ease;
    }

    .menu-toggle:hover,
    .menu-toggle[aria-expanded='true'] {
        color: var(--accent);
        border-color: rgba(199, 255, 73, 0.34);
        background: rgba(199, 255, 73, 0.04);
    }

    .menu-toggle__icon {
        position: relative;
        width: 1rem;
        height: 0.75rem;
    }

    .menu-toggle__icon i {
        position: absolute;
        left: 0;
        width: 100%;
        height: 1px;
        background: currentColor;
        transition: top 240ms var(--ease-out), transform 240ms var(--ease-out);
    }

    .menu-toggle__icon i:first-child {
        top: 0.2rem;
    }

    .menu-toggle__icon i:last-child {
        top: 0.58rem;
    }

    .menu-toggle[aria-expanded='true'] .menu-toggle__icon i:first-child,
    .menu-toggle[aria-expanded='true'] .menu-toggle__icon i:last-child {
        top: 0.38rem;
    }

    .menu-toggle[aria-expanded='true'] .menu-toggle__icon i:first-child {
        transform: rotate(45deg);
    }

    .menu-toggle[aria-expanded='true'] .menu-toggle__icon i:last-child {
        transform: rotate(-45deg);
    }

    .category-nav {
        position: absolute;
        top: calc(100% + 0.75rem);
        right: 0;
        left: auto;
        width: min(22rem, 100%);
        height: auto;
        padding: 0.65rem;
        display: flex;
        flex-direction: column;
        align-items: stretch;
        gap: 0.2rem;
        border: 1px solid var(--line-strong);
        background: rgba(11, 13, 14, 0.96);
        box-shadow: 0 1.5rem 4rem rgba(0, 0, 0, 0.42);
        backdrop-filter: blur(18px);
        opacity: 0;
        visibility: hidden;
        transform: translateY(-0.5rem);
        transform-origin: top right;
        transition: opacity 220ms ease, visibility 220ms ease, transform 320ms var(--ease-out);
    }

    .category-nav::before {
        content: 'Navegação / 01—04';
        padding: 0.7rem 0.8rem 0.6rem;
        color: var(--accent);
        font: 400 0.55rem/1 'kodemono', monospace;
        letter-spacing: 0.14em;
        text-transform: uppercase;
    }

    .category-nav.is-open {
        opacity: 1;
        visibility: visible;
        transform: translateY(0);
    }

    .category-nav button {
        min-height: 3.25rem;
        padding: 0 0.8rem;
        border-top: 1px solid var(--line);
        text-align: left;
        font-size: 0.72rem;
    }

    .category-nav button::after {
        top: 50%;
        right: 0.8rem;
        bottom: auto;
        left: auto;
        width: 1.4rem;
        transform: scaleX(0) translateY(-50%);
    }

    .category-nav button.is-active::after {
        transform: scaleX(1) translateY(-50%);
    }

    .category-nav button.is-active {
        padding-left: 1.1rem;
        color: var(--accent);
    }

    .category-nav button.is-active::before {
        content: '';
        position: absolute;
        left: 0;
        width: 2px;
        height: 1rem;
        background: var(--accent);
    }

    .header-links {
        width: 100%;
        justify-content: space-between;
    }
}

@media (max-width: 460px) {
    .brand__name {
        display: none;
    }

    .category-nav__number {
        display: none;
    }

    .header-links__icon-button {
        display: none;
    }

    .header-links__icon-link {
        display: none;
    }

    .header-links .header-links__contact {
        margin-left: 0;
    }

    .header-links .header-links__contact span {
        display: none;
    }

    .header-links .header-links__contact {
        width: 2.5rem;
        justify-content: center;
        padding-inline: 0;
    }

    .category-nav {
        width: 100%;
    }
}

@keyframes header-in {
    from {
        opacity: 0;
        transform: translateY(-12px);
    }

    to {
        opacity: 1;
        transform: translateY(0);
    }
}
</style>
