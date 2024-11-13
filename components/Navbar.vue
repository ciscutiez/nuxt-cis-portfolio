<script setup>
import { ref } from 'vue'
import { useRoute } from 'vue-router'
import { Menu, X, Home, BookOpen, Briefcase, Settings } from 'lucide-vue-next'

const route = useRoute()
const isOpen = ref(false)

const navigation = [
  { name: 'Home', href: '/', current: route.name === 'index', icon: Home },
  { name: 'Blog', href: '/blog', current: route.name?.includes('blog'), icon: BookOpen },
  { name: 'Projects', href: '/projects', current: route.name === 'projects', icon: Briefcase },

]

const toggleMenu = () => {
  isOpen.value = !isOpen.value
}
</script>

<template>
  <nav class="bg-gradient-to-r from-gray-900 to-gray-800 shadow-lg">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="flex items-center justify-between h-16">
        <div class="flex items-center">
          <div class="flex-shrink-0">
            <h1 class="font-bold text-3xl text-white">Ciscutiez</h1>
          </div>
          <div class="hidden md:block">
            <div class="ml-10 flex items-baseline space-x-4">
              <a v-for="item in navigation" :key="item.name" :href="item.href" :class="[item.current
                ? 'bg-gray-700 text-white'
                : 'text-gray-300 hover:bg-gray-700 hover:text-white',
                'px-3 py-2 rounded-md text-sm font-medium flex items-center transition-colors duration-200']"
                :aria-current="item.current ? 'page' : undefined">
                <component :is="item.icon" class="w-4 h-4 mr-2" />
                {{ item.name }}
              </a>
            </div>
          </div>
        </div>
        <div class="md:hidden">
          <button @click="toggleMenu"
            class="inline-flex items-center justify-center p-2 rounded-md text-gray-400 hover:text-white hover:bg-gray-700 focus:outline-none focus:ring-2 focus:ring-inset focus:ring-white">
            <span class="sr-only">Open main menu</span>
            <Menu v-if="!isOpen" class="block h-6 w-6" aria-hidden="true" />
            <X v-else class="block h-6 w-6" aria-hidden="true" />
          </button>
        </div>
      </div>
    </div>

    <div :class="['md:hidden', isOpen ? 'block' : 'hidden']">
      <div class="px-2 pt-2 pb-3 space-y-1 sm:px-3">
        <a v-for="item in navigation" :key="item.name" :href="item.href" :class="[item.current
          ? 'bg-gray-700 text-white'
          : 'text-gray-300 hover:bg-gray-700 hover:text-white',
          ' px-3 py-2 rounded-md text-base font-medium flex items-center transition-colors duration-200']"
          :aria-current="item.current ? 'page' : undefined">
          <component :is="item.icon" class="w-5 h-5 mr-3" />
          {{ item.name }}
        </a>
      </div>
    </div>
  </nav>
</template>