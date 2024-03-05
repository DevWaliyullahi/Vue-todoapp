<template>
  <div id="app">
    <h1>My To-Do List</h1>
    <div> <TodoList /> </div>
  </div>
</template>

<script setup lang="ts">
import TodoList from './components/TodoList.vue';
</script>

<style>
@import './style.css';
</style>
