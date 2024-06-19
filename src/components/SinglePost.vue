<script setup>
defineProps(['post'])
</script>

<template>
    <div></div>
    <router-link :to="{ name: 'Details', params: { id: post.id } }">{{ post.title }}</router-link>
</template>

<style scoped>

</style>