<script setup>
defineProps({
    modelValue: {
        type: String,
        required: true,
    },
});

const emit = defineEmits(['update:modelValue']);

const categories = [
    { id: 'landing', label: 'Landing Pages' },
    { id: 'systems', label: 'Sistemas Web' },
    { id: 'apps', label: 'Apps' },
];
</script>

<template>
    <header class="site-header">
        <a class="brand" href="#" aria-label="Gean Lima — início">
            <span class="brand__mark" aria-hidden="true">G</span>
            <span class="brand__name">Gean Lima</span>
        </a>

        <nav class="category-nav" aria-label="Categorias do portfólio">
            <button
                v-for="(category, index) in categories"
                :key="category.id"
                type="button"
                :class="{ 'is-active': modelValue === category.id }"
                :aria-pressed="modelValue === category.id"
                @click="emit('update:modelValue', category.id)"
            >
                <span class="category-nav__number">0{{ index + 1 }}</span>
                {{ category.label }}
            </button>
        </nav>

        <div class="header-links" aria-label="Redes e contato">
            <a href="https://github.com/Gean-Lima" target="_blank" rel="noopener noreferrer" aria-label="GitHub">
                GH
            </a>
            <a href="https://www.linkedin.com/in/gean-lima-775b491a2/" target="_blank" rel="noopener noreferrer" aria-label="LinkedIn">
                IN
            </a>
            <a
                class="header-links__contact"
                href="https://www.linkedin.com/in/gean-lima-775b491a2/"
                target="_blank"
                rel="noopener noreferrer"
            >
                Vamos conversar
                <span aria-hidden="true">↗</span>
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
    display: grid;
    grid-template-columns: 1fr auto 1fr;
    align-items: center;
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
    gap: 0.8rem;
}

.header-links > a {
    color: var(--muted);
    font: 500 0.64rem/1 'kodemono', monospace;
    letter-spacing: 0.08em;
    text-decoration: none;
    transition: color 200ms ease;
}

.header-links > a:hover {
    color: var(--accent);
}

.header-links .header-links__contact {
    margin-left: 0.3rem;
    padding: 0.75rem 0.9rem;
    border: 1px solid var(--line-strong);
    color: var(--ink);
}

.header-links__contact span {
    display: inline-block;
    margin-left: 0.5rem;
    color: var(--accent);
    transition: transform 200ms ease;
}

.header-links__contact:hover span {
    transform: translate(2px, -2px);
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

    .category-nav__number,
    .header-links > a:not(.header-links__contact) {
        display: none;
    }

    .category-nav button {
        font-size: 0.65rem;
    }
}

@keyframes header-in {
    from { opacity: 0; transform: translateY(-12px); }
    to { opacity: 1; transform: translateY(0); }
}
</style>
