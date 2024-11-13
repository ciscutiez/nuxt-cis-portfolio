<script setup lang="ts">
import { ref } from 'vue'
import { Github, Linkedin, Twitter } from 'lucide-vue-next'

const year = ref(new Date().getFullYear())
</script>

<template>
    <footer class="bg-gradient-to-r from-gray-900 to-gray-800 text-white py-12">
        <div class="container mx-auto px-4">
            <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
                <div class="text-center md:text-left">
                    <h3 class="text-2xl font-bold mb-4">Francis Charles Gonzales</h3>
                    <p class="text-gray-400">Passionate developer building amazing web experiences.</p>
                </div>
                <div class="text-center">
                    <h4 class="text-xl font-semibold mb-4">Quick Links</h4>
                    <nav class="flex flex-col space-y-2">
                        <a href="#" class="text-gray-400 hover:text-white transition-colors duration-300">Home</a>
                        <a href="#" class="text-gray-400 hover:text-white transition-colors duration-300">About</a>
                        <a href="#" class="text-gray-400 hover:text-white transition-colors duration-300">Projects</a>
                        <a href="#" class="text-gray-400 hover:text-white transition-colors duration-300">Contact</a>
                    </nav>
                </div>
                <div class="text-center md:text-right">
                    <h4 class="text-xl font-semibold mb-4">Connect</h4>
                    <div class="flex justify-center md:justify-end space-x-4">
                        <a href="https://github.com" target="_blank" rel="noopener noreferrer"
                            class="text-gray-400 hover:text-white transition-colors duration-300">
                            <Github class="w-6 h-6" />
                            <span class="sr-only">GitHub</span>
                        </a>
                        <a href="https://linkedin.com" target="_blank" rel="noopener noreferrer"
                            class="text-gray-400 hover:text-white transition-colors duration-300">
                            <Linkedin class="w-6 h-6" />
                            <span class="sr-only">LinkedIn</span>
                        </a>
                        <a href="https://twitter.com" target="_blank" rel="noopener noreferrer"
                            class="text-gray-400 hover:text-white transition-colors duration-300">
                            <Twitter class="w-6 h-6" />
                            <span class="sr-only">Twitter</span>
                        </a>
                    </div>
                </div>
            </div>
            <div class="mt-8 pt-8 border-t border-gray-700 text-center">
                <p class="text-sm text-gray-400">&copy; {{ year }} Francis Charles Gonzales. All rights reserved.</p>
            </div>
        </div>
    </footer>
</template>