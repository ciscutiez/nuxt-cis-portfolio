<script setup>


const { path } = useRoute()

const { data } = await useAsyncData(`content-$${path}`, () => { return queryContent().where({ _path: path }).findOne() }
);</script>
<template>
    <ContentRenderer :value="data" />
    <div class="my-8"><a v-for="tag in data.tags" :key="tag" :href="`/blog/tags/${tag}`">{{ tag }}</a></div>
</template>
