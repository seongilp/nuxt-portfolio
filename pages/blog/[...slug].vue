<template>
    <article class="prose dark:prose-invert  max-w-none prose-pre:bg-white dark:prose-pre:bg-gray-800 prose-pre:text-gray-500 dark:prose-pre:text-gray-300">
        <ContentDoc>
            <template #not-found>
                <h1>not found (404)</h1>
            </template>
            <template v-slot="{doc}">
                <div class="grid grid-cols-6 gap-16">
                    <div :class="{'col-span-6 md:col-span-4': doc.toc, 'col-span-6': !doc.toc}">
                        <ContentRenderer :value="doc" />        
                    </div>
                    <div class="hidden md:col-span-2 md:block not-prose" v-if="doc.toc">
                        <aside class="stikcy top-8">
                            <div class="font-semibold mb-2">
                                Table of Contents
                            </div>
                            <nav>
                                <TocLinks :links="doc.body.toc.links" :active-id="activeId"/>
                            </nav>
                        </aside>
                    </div>
                </div>
            </template>
        </ContentDoc>
    </article>
</template>

<script setup>
onMounted(() => {
    let elements = []
    const callback = (entries) => {
                // console.log(entries)
                for (const entry of entries) {
                    if (entry.isIntersction) {
                        activeId.value = entry.target.id
                        break;
                    }
                }
            }
            const observer = new IntersectionObserver(callback, {
                root: null,
                threshold: 0.5
            })
    setTimeout(
        () => {

            elements = document.querySelectorAll('h2,h3')
            for (const element of elements) {
                observer.observe(element)
            }

        }, 150)
        onBeforeUnmount(() => {
                for (const element of elements) {
                    observer.unobserve(element)
                }
        })
})
</script>