<script setup lang="ts">
import Todo from './components/Todo.vue';
import { ref } from 'vue';
const input = ref('');
const todos = ref<{ id: string, content: string, done: boolean }[]>([]);

const addTodo = () => {
    todos.value = [...todos.value, { id: crypto.randomUUID(), content: input.value, done: false}];
    input.value = '';
}

const deleteTodo = (id: string) => {
    const result = todos.value.filter((todo) => todo.id !== id);
    todos.value = result;
}

const changeTodoStatus = (id: string) => {
    const result = [...todos.value]
    for(const todo of result) {
        if(todo.id === id) {
            todo.done = !todo.done;
        }
    }
    
    todos.value = result;
}

const changeTitle = (id: string, newTitle: string) => {
    const result = [...todos.value]
    for(const todo of result) {
        if(todo.id === id) {
            todo.content = newTitle;
        }
    }
    todos.value = result;
};



</script>

<template>
    <div class="actions">
        <button @click="addTodo"></button>
        <input type="text" v-model="input" @keypress.enter="addTodo" placeholder="Create a new todo...">
    </div>
    <ul>
        <li v-for="todo in todos">
            <Todo 
                :content="todo.content" 
                :on-delete="() => deleteTodo(todo.id)" 
                :on-change="() => changeTodoStatus(todo.id)" 
                :done="todo.done"
                :id="todo.id"
                @change-title = "changeTitle"
            />
        </li>
    </ul>
</template>

<style scoped>
    .actions {
        width: 40dvw;
        display: flex;
        align-items: center;
        gap: 1rem;
        background-color: #25273c;
        padding: 1rem;
        border-radius: .2rem;
    }

    ul {
        display: flex;
        flex-direction: column;
    }

    li:not(:last-child) {
        border-bottom: 1px solid #404366;
    }

    input {
        background: none;
        padding: .5rem;
        font-size: 1.2rem;
        border: none;
        outline: none;
    }

    button {
        padding: 0 0 0 0;
        width: 2rem;
        height: 2rem;
        border: #404366 2px solid;
        border-radius: 50%;
        background: none;
    }

    li {
        display: flex;
        flex-direction: column;
        background-color: #25273c;
        padding: 1rem;
    }
</style>
