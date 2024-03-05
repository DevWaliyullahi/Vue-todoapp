<template>
    <div>
      <input type="checkbox" v-model="todo.completed" @change="toggleCompletion">
      <span :class="{ 'completed': todo.completed }">{{ todo.text }}</span>
      <button @click="removeTodo">Remove</button>
    </div>
  </template>
  
  <script setup lang="ts">
  import { defineProps, defineEmits } from 'vue';
  
  const props = defineProps<{
    todo: {
      id: number;
      text: string;
      completed: boolean;
    };
  }>();
  
  const { emit }  = defineEmits(['toggle', 'remove']);
  
  const toggleCompletion = () => {
    emit('toggle', props.todo.id);
  };
  
  const removeTodo = () => {
    emit('remove', props.todo.id);
  };
  </script>
  
  <style scoped>
    @import '../style.css';

  </style>
  