<script setup>
import PostList from "@/components/PostList.vue";
import getPosts from "@/composables/getPosts";
import Spinner from "@/components/Spinner.vue";

const {posts, error, load} = getPosts();
load()
</script>

<template>
    <div class="home">
        <h1>Home</h1>
        <div v-if="error">{{ error }}</div>
        <div v-if="posts.length">
            <PostList :posts="posts"/>
        </div>
        <div v-else>
            <Spinner />
        </div>
    </div>
</template>

<style scoped>
    .home {
        max-width: 1200px;
        margin: 0 auto;
        padding: 10px;
    }
</style>