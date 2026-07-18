<script setup>
import IconMark from '@/components/ui/IconMark.vue';

defineProps({
    modelValue: {
        type: String,
        required: true,
    },
});

const emit = defineEmits(['update:modelValue']);

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
    <header class="site-header">
        <nav class="category-nav" aria-label="Categorias do portfólio">
            <button
                v-for="(category, index) in categories"
                :key="category.id"
                type="button"
                :class="{ 'is-active': modelValue === category.id }"
                :aria-pressed="modelValue === category.id"
                @click="emit('update:modelValue', category.id)"
            >
                {{ category.label }}
            </button>
        </nav>

        <div class="header-links" aria-label="Redes e contato">
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
        height: var(--header-height);
        min-height: 0;
        grid-template-columns: 1fr auto;
        grid-template-rows: calc(var(--header-height) - 2.8rem) 2.8rem;
    }

    .category-nav {
        grid-row: 2;
        grid-column: 1 / -1;
        justify-content: space-between;
        gap: 0.75rem;
    }

    .header-links .header-links__contact {
        display: none;
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

    .category-nav button {
        font-size: 0.65rem;
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
