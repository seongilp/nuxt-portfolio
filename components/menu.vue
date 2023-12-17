<template>
    <nav class="font-mono">
        <ul class="flex flex-col md:flex-row md:space-x-4">
            <li>
                <nuxt-link to="/" class="link">Home</nuxt-link>
            </li>
            <li>
                <nuxt-link to="/about" class="link">About</nuxt-link>
            </li>
            <li>
                <nuxt-link to="/projects" class="link">Projects</nuxt-link>
            </li>
            <li>
                <nuxt-link to="/blog" class="link">blog</nuxt-link>
            </li>
        </ul>
    </nav>
</template>

<style scoped>
    .link {
        @apply p-1 hover:bg-gray-200 dark:hover:bg-gray-800 text-2xl md:text-base
    }
</style>