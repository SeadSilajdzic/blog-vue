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

<script setup>
import PostList from "@/components/PostList.vue";
import getPosts from "@/composables/getPosts";
import Spinner from "@/components/Spinner.vue";

const {posts, error, load} = getPosts();
load()
</script>
