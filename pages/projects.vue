<script setup>
const query = gql`
  query {
    viewer {
      repositories(first: 10, orderBy: {field: CREATED_AT, direction: DESC}) {
        totalCount
        nodes {
          id
          name
          createdAt
          description
          url
          forks {
            totalCount
          }
          watchers {
            totalCount
          }
          stargazers {
            totalCount
          }
        }
      }
    }
  }
`

const { data, } = await useAsyncQuery(query)

const formatDate = (dateString) => {
    return new Date(dateString).toLocaleDateString('en-US', {
        year: 'numeric',
        month: 'long',
        day: 'numeric'
    })
}
</script>

<template>
    <div class="px-4 py-8 bg-stone-50 min-h-screen">
        <div class="max-w-7xl mx-auto">
            <h1 class="text-4xl font-bold mb-4 text-stone-800">Projects</h1>
            <p class="text-xl mb-8 text-stone-600">Here are some of my projects on GitHub.</p>

            <div v-if="data" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                <div v-for="project in data.viewer.repositories.nodes" :key="project.id"
                    class="bg-stone-700/70 rounded-lg shadow-md hover:shadow-lg transition-all duration-300 hover:-translate-y-1">
                    <div class="p-6">
                        <h2 class="text-2xl font-semibold mb-2">
                            <a :href="project.url" target="_blank" rel="noopener noreferrer"
                                class="text-white hover:underline">
                                {{ project.name }}
                            </a>
                        </h2>
                        <p class="text-sm text-stone-300 mb-4">
                            Created on {{ formatDate(project.createdAt) }}
                        </p>
                        <p class="text-white mb-4 line-clamp-3">{{ project.description }}</p>
                        <div class="flex justify-between text-sm text-white">
                            <div class="flex items-center space-x-2">
                                <!-- <Star class="w-4 h-4 text-yellow-400" /> -->
                                <span>Stars: {{ project.stargazers.totalCount }}</span>
                            </div>
                            <div class="flex items-center space-x-2">
                                <!-- <GitFork class="w-4 h-4 text-green-400" /> -->
                                <span>Forks: {{ project.forks.totalCount }}</span>
                            </div>
                            <div class="flex items-center space-x-2">
                                <!-- <Eye class="w-4 h-4 text-blue-400" /> -->
                                <span>Watching: {{ project.watchers.totalCount }}</span>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <div v-else class="text-center text-stone-600">No projects found.</div>
        </div>
    </div>
</template>