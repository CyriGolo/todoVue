<script setup lang="ts">
    import { ref } from 'vue';
    interface I {
        content: string,
        onDelete: () => void,
        onChange: () => void,
        done: boolean,
        id: string
    }
    const props = defineProps<I>()

    const title = ref(props.content);
</script>

<template>
    <div class="container">
        <div>
            <input type="checkbox" :checked="props.done" @change="props.onChange" />
            <input type="text" v-model="title" @input="$emit('changeTitle', props.id, title)" :class="props.done ? 'done' : ''">
        </div>
        <button @click="props.onDelete">🗑️</button>
    </div>
</template>

<style scoped>
    div {
        display: flex;
        align-items: center;
        gap: 1rem;
    }

    .container {
        justify-content: space-between;
    }
    
    .done {
        text-decoration: line-through;
    }

    input[type="checkbox"] {
        padding: 0 0 0 0;
        width: 2rem;
        height: 2rem;
        border: #404366 2px solid;
        border-radius: 50%;
        background: none;
    }

    input[type="text"] {
        background: none;
        padding: .5rem;
        font-size: 1.2rem;
        border: none;
        outline: none;
    }

    button {
        border-color: #646cff38;
        opacity: 0;
        background: none;
        transition: .2s;
    }

    button:hover {
        border-color: #646cff;
    }

    li:hover button {
        opacity: 100%;
    }
</style>
