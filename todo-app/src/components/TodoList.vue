<template>
    <div>
      <input type="text" v-model="newTodoText" @keyup.enter="addTodo">
      <div v-for="todo in todos" :key="todo.id">
        <TodoItem :todo="todo" @toggle="toggleCompletion" @remove="removeTodo" />
      </div>
    </div>
  </template>
  
  <script setup lang="ts">
  import { ref } from 'vue';
  import TodoItem from './TodoItem.vue';
  
  const todos = ref<{ id: number; text: string; completed: boolean }[]>([]);
  const newTodoText = ref('');
  
  const addTodo = () => {
    if (newTodoText.value.trim() !== '') {
      todos.value.push({ id: Date.now(), text: newTodoText.value, completed: false });
      newTodoText.value = '';
    }
  };
  
  const toggleCompletion = (todoId: number) => {
    const todo = todos.value.find(todo => todo.id === todoId);
    if (todo) todo.completed = !todo.completed;
  };
  
  const removeTodo = (todoId: number) => {
    todos.value = todos.value.filter(todo => todo.id !== todoId);
  };
  </script>
  
  <style scoped>
  @import '../style.css';
  </style>
  