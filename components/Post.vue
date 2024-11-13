<script setup>
import { defineProps } from 'vue'


const props = defineProps({
    posts: {
        type: Array,
        required: true
    }
})


</script>

<template>
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
        <article v-for="post in props.posts" :key="post.slug"
            class="bg-white rounded-xl shadow-lg overflow-hidden transition-all duration-300 hover:shadow-2xl hover:-translate-y-1">
            <NuxtLink :to="post._path" class="block">
                <div class="relative">
                    <img v-if="post.cover" :src="post.cover" :alt="post.title" class="w-full h-56 object-cover" />
                    <div v-else class="w-full h-56 bg-gradient-to-br from-blue-400 to-indigo-600"></div>
                    <div class="absolute bottom-0 left-0 right-0 p-4 bg-gradient-to-t from-black/70 to-transparent">
                        <h2 class="text-xl font-bold text-white mb-2 line-clamp-2">{{ post.title }}</h2>
                    </div>
                </div>
                <div class="p-6">
                    <p class="text-gray-600 mb-4 line-clamp-3">{{ post.description }}</p>
                    <div class="flex items-center justify-between text-sm text-gray-500">

                        <span
                            class="inline-flex items-center text-blue-600 font-medium hover:text-blue-800 transition-colors duration-200">
                            Read More
                            <ChevronRight class="w-4 h-4 ml-1" />
                        </span>
                    </div>
                </div>
            </NuxtLink>
        </article>
    </div>
</template>