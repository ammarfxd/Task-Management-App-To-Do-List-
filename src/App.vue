<script setup>
import { ref } from 'vue'
import { useTodoStore } from './stores/todo'

const todoStore = useTodoStore()
const newTodo = ref('')

function addNewTodo() {
  if (newTodo.value.trim()) {
    todoStore.addTodo(newTodo.value)
    newTodo.value = ''
  }
}
</script>

<template>
  <div class="container">
    <h1>My To-Do List</h1>

    <div class="input-group">
      <input v-model="newTodo" @keyup.enter="addNewTodo" placeholder="What are your plans?" />
      <button @click="addNewTodo">Add</button>
    </div>

    <p>Total: {{ todoStore.totalTasks }} | Completed: {{ todoStore.completedTasks }}</p>

    <ul>
      <li v-for="todo in todoStore.todos" :key="todo.id" :class="{ done: todo.completed }">
        <span @click="todoStore.toggleTodo(todo.id)">
          {{ todo.text }}
        </span>
        <button @click="todoStore.removeTodo(todo.id)">Delete</button>
      </li>
    </ul>
  </div>
</template>

<style scoped>
  .done {
  text-decoration: line-through;
  color: gray;
}
.container {
  max-width: 400px;
  margin: 50px auto;
  font-family: sans-serif;
}
.input-group {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}
li {
  display: flex;
  justify-content: space-between;
  padding: 8px 0;
  border-bottom: 1px solid #eee;
  cursor: pointer;
}
</style>
