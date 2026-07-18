<script setup>
const stacks = ['Laravel', 'Vue.js', 'Nuxt', 'Flutter', 'PHP', 'MySQL'];
</script>

<template>
    <footer class="profile-strip">
        <div class="profile-strip__experience">
            <span class="profile-strip__label">Experiência</span>
            <p>
                <strong>2018—Agora</strong>
                <span class="profile-strip__role">Desenvolvimento full-stack</span>
                <span class="profile-strip__mobile-stack">Laravel · Vue · Flutter</span>
            </p>
        </div>

        <div class="profile-strip__stack">
            <span class="profile-strip__label">Stack principal</span>
            <ul aria-label="Tecnologias principais">
                <li v-for="stack in stacks" :key="stack">{{ stack }}</li>
            </ul>
        </div>

        <a href="https://github.com/Gean-Lima" target="_blank" rel="noopener noreferrer">
            GitHub
            <span aria-hidden="true">↗</span>
        </a>
    </footer>
</template>

<style lang="scss">
.profile-strip {
    min-height: var(--strip-height);
    display: grid;
    grid-template-columns: 0.8fr 1.4fr auto;
    align-items: center;
    gap: clamp(1.5rem, 4vw, 4rem);
    border-top: 1px solid var(--line);
    animation: strip-in 800ms 450ms var(--ease-out) both;
}

.profile-strip__experience,
.profile-strip__stack {
    min-width: 0;
    display: flex;
    align-items: center;
    gap: clamp(0.8rem, 1.7vw, 1.5rem);
}

.profile-strip__label {
    color: var(--muted);
    font: 400 0.55rem/1 'kodemono', monospace;
    letter-spacing: 0.13em;
    text-transform: uppercase;
    white-space: nowrap;
}

.profile-strip p {
    margin: 0;
    overflow: hidden;
    color: var(--muted-light);
    font: 400 0.68rem/1.4 'kodemono', monospace;
    text-overflow: ellipsis;
    white-space: nowrap;
}

.profile-strip p strong {
    margin-right: 0.65rem;
    color: var(--ink);
    font-weight: 400;
}

.profile-strip__mobile-stack {
    display: none;
}

.profile-strip ul {
    margin: 0;
    padding: 0;
    display: flex;
    align-items: center;
    gap: clamp(0.65rem, 1.2vw, 1.2rem);
    list-style: none;
}

.profile-strip li {
    color: var(--muted-light);
    font: 400 0.66rem/1 'kodemono', monospace;
    white-space: nowrap;
}

.profile-strip li::before {
    content: '';
    width: 3px;
    aspect-ratio: 1;
    margin-right: 0.45rem;
    display: inline-block;
    border-radius: 50%;
    background: var(--accent);
    vertical-align: middle;
}

.profile-strip > a {
    color: var(--ink);
    font: 400 0.65rem/1 'kodemono', monospace;
    letter-spacing: 0.06em;
    text-decoration: none;
}

.profile-strip > a span {
    display: inline-block;
    margin-left: 0.4rem;
    color: var(--accent);
    transition: transform 200ms ease;
}

.profile-strip > a:hover span {
    transform: translate(2px, -2px);
}

@keyframes strip-in {
    from { opacity: 0; transform: translateY(12px); }
    to { opacity: 1; transform: translateY(0); }
}

@media (max-width: 900px) {
    .profile-strip {
        grid-template-columns: 1fr auto;
    }

    .profile-strip__stack {
        display: none;
    }
}

@media (max-width: 520px) {
    .profile-strip {
        gap: 0.75rem;
    }

    .profile-strip__experience {
        display: grid;
        gap: 0.4rem;
    }

    .profile-strip p span,
    .profile-strip p strong {
        margin-right: 0.35rem;
    }

    .profile-strip__role {
        display: none;
    }

    .profile-strip__mobile-stack {
        display: inline;
    }
}
</style>
