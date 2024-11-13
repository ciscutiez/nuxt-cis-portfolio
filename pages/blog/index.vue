<script setup>
import { ref, computed } from 'vue'


const { data: posts } = await useAsyncData('posts', () =>
    queryContent('/blog').sort({ date: -1 }).find()
)

const searchQuery = ref('')
const currentPage = ref(1)
const postsPerPage = 9

const filteredPosts = computed(() => {
    return posts.value?.filter(post =>
        post.title.toLowerCase().includes(searchQuery.value.toLowerCase()) ||
        post.description.toLowerCase().includes(searchQuery.value.toLowerCase())
    ) || []
})

const paginatedPosts = computed(() => {
    const start = (currentPage.value - 1) * postsPerPage
    const end = start + postsPerPage
    return filteredPosts.value.slice(start, end)
})

const totalPages = computed(() => Math.ceil(filteredPosts.value.length / postsPerPage))

function changePage(newPage) {
    currentPage.value = newPage
}

function formatDate(date) {
    return new Date(date).toLocaleDateString('en-US', { year: 'numeric', month: 'long', day: 'numeric' })
}
</script>

<template>
    <div class="container mx-auto px-4 py-12">
        <h1 class="text-4xl md:text-5xl font-bold text-center text-gray-800 mb-12">Blog Posts</h1>

        <div class="mb-8 relative">
            <input v-model="searchQuery" type="text" placeholder="Search blog posts..."
                class="w-full px-4 py-2 pl-10 pr-4 rounded-full border border-gray-300 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent" />
            <Search class="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400" />
        </div>

        <section v-if="paginatedPosts.length > 0" class="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
            <article v-for="post in paginatedPosts" :key="post._path"
                class="bg-white rounded-lg shadow-md overflow-hidden transition-all duration-300 hover:shadow-xl hover:-translate-y-1">
                <NuxtLink :to="post._path" class="block">
                    <img v-if="post.cover" :src="post.cover" :alt="post.title" class="w-full h-48 object-cover" />
                    <div v-else class="w-full h-48 bg-gradient-to-br from-blue-400 to-indigo-600"></div>
                    <div class="p-6">
                        <h2 class="text-xl font-bold text-gray-800 mb-2 line-clamp-2">{{ post.title }}</h2>
                        <p class="text-gray-600 mb-4 line-clamp-3">{{ post.description }}</p>
                        <div class="flex justify-between items-center text-sm text-gray-500">
                         
                            <span class="inline-flex items-center text-blue-600 hover:text-blue-800">
                                Read More
                                <ChevronRight class="w-4 h-4 ml-1" />
                            </span>
                        </div>
                    </div>
                </NuxtLink>
            </article>
        </section>

        <div v-else class="text-center text-gray-600 py-12">
            <p class="text-xl">No blog posts found matching your search.</p>
        </div>

        <div v-if="totalPages > 1" class="mt-12 flex justify-center space-x-2">
            <button @click="changePage(currentPage - 1)" :disabled="currentPage === 1"
                class="px-4 py-2 rounded-md bg-gray-200 text-gray-800 disabled:opacity-50">
                <ChevronLeft class="w-5 h-5" />
            </button>
            <button v-for="page in totalPages" :key="page" @click="changePage(page)" :class="[
                'px-4 py-2 rounded-md',
                currentPage === page ? 'bg-blue-600 text-white' : 'bg-gray-200 text-gray-800'
            ]">
                {{ page }}
            </button>
            <button @click="changePage(currentPage + 1)" :disabled="currentPage === totalPages"
                class="px-4 py-2 rounded-md bg-gray-200 text-gray-800 disabled:opacity-50">
                <ChevronRight class="w-5 h-5" />
            </button>
        </div>
    </div>
</template>