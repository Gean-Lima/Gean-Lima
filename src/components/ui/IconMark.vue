<script setup>
defineProps({
    name: {
        type: String,
        required: true,
    },
});
</script>

<template>
    <svg v-if="name === 'github'" viewBox="0 0 24 24" aria-hidden="true" focusable="false">
        <path
            d="M12 2a10 10 0 0 0-3.16 19.48c.5.09.68-.22.68-.48v-1.7c-2.78.61-3.37-1.34-3.37-1.34-.46-1.18-1.12-1.49-1.12-1.49-.92-.63.07-.62.07-.62 1.02.08 1.56 1.05 1.56 1.05.9 1.54 2.36 1.1 2.93.85.09-.65.35-1.1.63-1.35-2.22-.25-4.56-1.11-4.56-4.92 0-1.09.38-1.98 1.02-2.68-.1-.25-.44-1.26.1-2.62 0 0 .84-.27 2.75 1.02a9.5 9.5 0 0 1 5 0c1.9-1.29 2.75-1.02 2.75-1.02.54 1.36.2 2.37.1 2.62.63.7 1.02 1.59 1.02 2.68 0 3.82-2.35 4.66-4.58 4.91.36.31.67.92.67 1.86v2.75c0 .26.18.57.69.48A10 10 0 0 0 12 2Z"
        />
    </svg>

    <svg v-else-if="name === 'linkedin'" viewBox="0 0 24 24" aria-hidden="true" focusable="false">
        <path
            d="M5.3 8.4h3.3v10.2H5.3V8.4Zm1.7-5A1.95 1.95 0 1 1 5.05 7a1.95 1.95 0 0 1 1.95-3.6ZM12 8.4h3.16v1.39h.04c.44-.84 1.52-1.72 3.13-1.72 3.35 0 3.97 2.2 3.97 5.06v5.49h-3.3v-4.86c0-1.16-.02-2.65-1.61-2.65-1.62 0-1.87 1.26-1.87 2.56v4.95H12V8.4Z"
        />
    </svg>

    <svg v-else-if="name === 'whatsapp'" viewBox="0 0 24 24" aria-hidden="true" focusable="false">
        <path
            d="M12.02 2a9.97 9.97 0 0 0-8.67 15l-1.22 4.45 4.57-1.2A10 10 0 1 0 12.02 2Zm5.83 14.45c-.25.7-1.28 1.28-1.75 1.36-.47.08-1.08.12-1.74-.08-.4-.12-.9-.28-1.54-.55-2.7-1.17-4.46-3.88-4.59-4.06-.12-.18-1.1-1.46-1.1-2.79 0-1.33.69-1.99.94-2.26.25-.27.55-.33.73-.33.18 0 .36 0 .52.01.17.01.4-.06.62.47.25.58.84 2.01.91 2.16.07.15.12.33.02.52-.1.18-.15.29-.3.45-.15.17-.32.37-.46.49-.15.15-.31.31-.13.62.18.3.79 1.3 1.7 2.11 1.17 1.05 2.16 1.38 2.47 1.53.3.15.48.13.65-.08.17-.2.73-.85.92-1.14.19-.3.38-.25.65-.15.27.1 1.72.81 2.02.96.3.15.49.23.56.36.08.13.08.75-.17 1.45Z"
        />
    </svg>

    <svg v-else-if="name === 'laravel'" viewBox="0 0 24 24" aria-hidden="true" focusable="false">
        <path
            d="M12 2.7 5.1 6.3v11.4L12 21.3l6.9-3.6V6.3L12 2.7Zm0 2.1 5 2.6-5 2.6-5-2.6 5-2.6Zm-5 4.8 5 2.6v5.3l-5-2.6V9.6Zm10 0v5.3l-5 2.6v-5.3l5-2.6Z"
        />
    </svg>

    <svg v-else-if="name === 'vue'" viewBox="0 0 24 24" aria-hidden="true" focusable="false">
        <path
            d="M12 3 2.8 3l9.2 16 9.2-16H17l-5 8.5L7 3H4.9L12 15.8 19.1 3H17l-5 8.5L7 3Z"
        />
    </svg>

    <svg v-else-if="name === 'nuxt'" viewBox="0 0 24 24" aria-hidden="true" focusable="false">
        <path
            d="m12 4.3 8.5 14.7H3.5L12 4.3Zm0 4.5-5.1 8.9h10.2L12 8.8Z"
        />
    </svg>

    <svg v-else-if="name === 'flutter'" viewBox="0 0 24 24" aria-hidden="true" focusable="false">
        <path
            d="M6.7 13.2 12 18.5l3.2-3.2-5.4-5.4-3.1 3.3Zm5.3 5.3 1.6 1.6h4.8l-4-4-2.4 2.4Zm0-13.1L4.3 13l2.4 2.4 10-10.1h-4.7Z"
        />
    </svg>

    <svg v-else-if="name === 'php'" viewBox="0 0 24 24" aria-hidden="true" focusable="false">
        <path
            d="M7 7.5h4.2c2.2 0 3.7 1.1 3.7 3s-1.4 3.2-3.7 3.2H9.2l-.5 2.8H6L7 7.5Zm2.2 4.3h1.7c.8 0 1.5-.3 1.5-1.1 0-.8-.6-1.1-1.5-1.1H9.7l-.5 2.2Z"
        />
    </svg>

    <svg v-else-if="name === 'mysql'" viewBox="0 0 24 24" aria-hidden="true" focusable="false">
        <path
            d="M12 3.4c-3.3 0-6 1.4-6 3.2v10.8c0 1.8 2.7 3.2 6 3.2s6-1.4 6-3.2V6.6c0-1.8-2.7-3.2-6-3.2Zm0 2c2.7 0 4 .8 4 1.2S14.7 7.8 12 7.8 8 7 8 6.6 9.3 5.4 12 5.4Zm4 12c0 .4-1.3 1.2-4 1.2s-4-.8-4-1.2V9.4c1.1.7 2.8 1.1 4 1.1s2.9-.4 4-1.1v8Z"
        />
    </svg>

    <svg v-else-if="name === 'arrow-up-right'" viewBox="0 0 24 24" aria-hidden="true" focusable="false">
        <path
            d="M7 17.5V15.7l7.9-7.9H13V5.5h8.5V14h-2.3V11.1L11.3 19H7Z"
        />
    </svg>

    <svg v-else-if="name === 'chip'" viewBox="0 0 24 24" aria-hidden="true" focusable="false">
        <path
            d="M8 8h8v8H8V8Zm-3 3h2M3 13h2m14-2h2m-2 4h2M11 3v2m2-2v2m-2 14v2m2-2v2"
        />
    </svg>

    <svg v-else viewBox="0 0 24 24" aria-hidden="true" focusable="false">
        <path d="M4 12h16" />
        <path d="M12 4l8 8-8 8" />
    </svg>
</template>

<style scoped>
svg {
    width: 100%;
    height: 100%;
    fill: none;
    stroke: currentColor;
    stroke-width: 1.8;
    stroke-linecap: round;
    stroke-linejoin: round;
}

svg path {
    fill: currentColor;
    stroke: none;
}

svg [stroke] {
    fill: none;
}
</style>
