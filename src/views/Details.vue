<script setup>
import getPost from "@/composables/getPost";
import Spinner from "@/components/Spinner.vue";

const props = defineProps(['id'])
const {post, error, load} = getPost(props.id)
load()
</script>

<template>
    <div v-if="error">{{ error }}</div>
    <div v-if="post" class="post">
        <h3>{{ post.title }}</h3>
        <p class="pre">{{ post.body }}</p>
    </div>

    <div v-else>
        <Spinner />
    </div>
</template>

<style scoped>
    .post {
        max-width: 1200px;
        margin: 0 auto;
    }

    .post p {
        color: #444;
        line-height: 1.5em;
        margin-top: 40px;
    }

    .pre {
        white-space: pre-wrap;
    }
</style>