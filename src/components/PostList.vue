<script setup>
import SinglePost from "@/components/SinglePost.vue";

defineProps(['posts'])
</script>

<template>
    <div class="post-list">
        <div v-for="post in posts" :key="post.id">
            <SinglePost :post="post" />
        </div>
    </div>
</template>

<style scoped>

</style>