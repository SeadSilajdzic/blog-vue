<script setup>
import {ref} from "vue";

const title = ref('');
const body = ref('');
const tag = ref('');
const tags = ref([]);

const handleKeydown = () => {
    if (!tags.value.includes(tag.value)) {
        tag.value = tag.value.replace(/\s/, '');
        tags.value.push(tag.value);
    }

    tag.value = '';
}

const addPost = async () => {
    await fetch("http://localhost:3000/posts", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({
            title: title.value,
            body: body.value,
            tags: tags.value,
        })
    })

    title.value = '';
    body.value = '';
    tags.value = [];
}
</script>

<template>
    <div class="create">
        <form @submit.prevent="addPost">
            <label>Title</label>
            <input v-model="title" type="text" required>

            <label>Content</label>
            <textarea v-model="body" required></textarea>

            <label>Tags (hit enter to add a tag)</label>
            <input v-model="tag" @keydown.enter.prevent="handleKeydown" type="text">

            <div v-for="tag in tags" :key="tag" class="pill">#{{ tag }}</div>

            <button>Add Post</button>
        </form>
    </div>
</template>

<style scoped>
form {
    max-width: 480px;
    margin: 0 auto;
    text-align: left;
}

input, textarea {
    display: block;
    margin: 10px 0;
    width: 100%;
    box-sizing: border-box;
    padding-bottom: 10px;
    border: 1px solid #eee;
}

textarea {
    height: 160px;
}

label {
    display: inline-block;
    margin-top: 30px;
    position: relative;
    font-size: 20px;
    color: white;
    margin-bottom: 10px;
}

label::before {
    content: "";
    display: block;
    width: 100%;
    height: 100%;
    position: absolute;
    background: #ff8800;
    z-index: -1;
    padding-right: 40px;
    left: -30px;
    transform: rotateZ(-1.5deg);
}

button {
    display: block;
    margin-top: 30px;
    background: #ff8800;
    color: white;
    border: none;
    padding: 8px 16px;
    font-size: 18px;
    cursor: pointer;
}

.pill {
    display: inline-block;
    margin: 10px 10px 0 0;
    color: #444;
    background: #ddd;
    padding: 8px;
    border-radius: 20px;
    font-size: 14px;
}
</style>