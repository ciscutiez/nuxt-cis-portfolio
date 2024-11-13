<script setup>
import { ref } from 'vue'


const message = ref("Hi, I'm Francis Charles Gonzales")

const { data: posts } = await useAsyncData('latest-post', () =>
    queryContent("/blog").sort({ date: -1 }).limit(3).find()
)
</script>

<template>
    <div class="min-h-screen w-full bg-gradient-to-br from-gray-100 to-gray-200">
        <section class=" py-20 flex flex-col items-center justify-center text-center">
            <h1 class="text-5xl md:text-6xl font-extrabold text-gray-800 mb-6 animate-fade-in-up">
                {{ message }}
            </h1>
            <p class="text-xl text-gray-600 max-w-2xl mb-10 animate-fade-in-up animation-delay-200">
                I'm a frontend, full-stack, and mobile developer with expertise in technologies like
                Vue, React, Next.js, and React Native, as well as back-end frameworks like Node.js.
                I specialize in creating seamless user experiences and efficient, scalable solutions.
            </p>
            <div
                class="flex flex-col sm:flex-row space-y-4 sm:space-y-0 sm:space-x-4 animate-fade-in-up animation-delay-400">
                <a href="/projects"
                    class="inline-flex items-center justify-center px-6 py-3 border border-transparent text-base font-medium rounded-md text-white bg-blue-600 hover:bg-blue-700 transition duration-300 ease-in-out transform hover:-translate-y-1">
                    View My Projects
                    <ChevronRight class="ml-2 h-5 w-5" />
                </a>
                <a href="/contact"
                    class="inline-flex items-center justify-center px-6 py-3 border border-transparent text-base font-medium rounded-md text-blue-600 bg-white hover:bg-gray-50 transition duration-300 ease-in-out transform hover:-translate-y-1">
                    Get In Touch
                </a>
            </div>
        </section>

        <section class="container mx-auto px-4 py-20">
            <h2 class="text-3xl font-bold text-gray-800 mb-8 text-center">Latest Blog Posts</h2>
            <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
                <div v-for="post in posts" :key="post._path"
                    class="bg-white rounded-lg shadow-md overflow-hidden transition duration-300 ease-in-out transform hover:-translate-y-1 hover:shadow-xl">
                    <img v-if="post.cover" :src="post.cover" :alt="post.title" class="w-full h-48 object-cover" />
                    <div class="p-6">
                        <h3 class="text-xl font-semibold text-gray-800 mb-2">{{ post.title }}</h3>
                        <p class="text-gray-600 mb-4">{{ post.description }}</p>
                        <div class="flex items-center justify-between">
                            
                            <a :href="post._path" class="inline-flex items-center text-blue-600 hover:text-blue-800">
                                Read More
                                <!-- <ChevronRight class="ml-1 h-4 w-4" /> -->
                            </a>
                        </div>
                    </div>
                </div>
            </div>
            <div class="text-center mt-12">
                <a href="/blog"
                    class="inline-flex items-center justify-center px-6 py-3 border border-transparent text-base font-medium rounded-md text-white bg-blue-600 hover:bg-blue-700 transition duration-300 ease-in-out">
                    <Newspaper class="mr-2 h-5 w-5" />
                    View All Posts
                </a>
            </div>
        </section>
    </div>
</template>

<style scoped>
@keyframes fadeInUp {
    from {
        opacity: 0;
        transform: translateY(20px);
    }

    to {
        opacity: 1;
        transform: translateY(0);
    }
}

.animate-fade-in-up {
    animation: fadeInUp 0.6s ease-out forwards;
}

.animation-delay-200 {
    animation-delay: 0.2s;
}

.animation-delay-400 {
    animation-delay: 0.4s;
}
</style>