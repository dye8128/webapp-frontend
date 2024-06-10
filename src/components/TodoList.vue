<script setup lang="ts">
import { ref } from 'vue'

interface Todo {
    task: string
    done: boolean
}

const todos = ref<Todo[]>([
    { task: '牛乳を買う', done: false },
    { task: 'Vue 3の勉強をする', done: true }
])

const newTodoTask = ref('')
const addTodo = () => {
    if (newTodoTask.value === ''){
        alert('タスクを入力してください')
        return
    }
    todos.value.push({ task: newTodoTask.value, done: false })
    newTodoTask.value = ''
}

const finishTask = (task: string) => {
    const todo = todos.value.find(todo => todo.task === task)
    if (todo) todo.done = true
}
</script>

<template>
    <div>
        <h2>TodoList</h2>
        未完タスク
        <ul>
            <template v-for="todo in todos" :key="todo.task">
                <li v-if="!todo.done">
                    <div>{{ todo.task }}</div>
                    <button @click="finishTask(todo.task)">完了する</button>
                </li>
            </template>
        </ul>
        完了済タスク
        <ul>
            <template v-for="todo in todos" :key="todo.task">
                <li v-if="todo.done">{{ todo.task }}</li>
            </template>
        </ul>
        <div>
            <label>
                タスク
                <input v-model="newTodoTask" type="text" />
            </label>
            <button @click="addTodo">追加</button>
        </div>
    </div>
</template>