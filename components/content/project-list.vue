<template>
<div class="not-prose">
    <p class="mb-10">Take a look at nuxt github projects</p>
    <section v-if="pending">Loading..</section>
    <section v-else-if="error">Something went wrong... Try again</section>
    <section v-else>Here we display</section>
    <section v-else>
        <ul class="grid grid-cols-1 gap-4">
            <li v-for="repository in repos" :key="repository.id" class="border border-gray-200 rounded-sm p-4 hover:bg-gray-100 dark:hover:bg-gray-800 font-mono dark:border-gray-800">
                <a :href="repository.html_url" target="_blank" class="text-xl font-semibold">
                    <div class="flex items-center justify-between">
                        <div class="font-semibold">
                            {{ repository.name }}
                        </div>
                        <div>
                            {{ repository.stargazers_count }} * 
                        </div>
                    </div>
                </a>
                <p class="text-gray-500 text-sm">{{ repository.description }}</p>
            </li>
        </ul>
    </section>
</div>
</template>

<script setup>
    const {error, pending, data} = await useFetch('https://api.github.com/users/nuxt/repos')
    const repos = computed( 
        () => data.value.filter(repo => repo.description)
        .sort((a,b) => b.stargazers_count - a.stargazers_count)
    )
</script>