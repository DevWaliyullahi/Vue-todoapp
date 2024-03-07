<template>
    <div>
      <input type="checkbox" v-model="todo.completed" @change="toggleCompletion">
      <span :class="{ 'completed': todo.completed }">{{ todo.text }}</span>
      <button @click="removeTodo">Remove</button>
    </div>
  </template>
<script setup lang="ts">

import { defineProps } from 'vue';

const props = defineProps<{
  todo: {
    id: number;
    text: string;
    completed: boolean;
  };
}>();

// Use type assertion to specify the type of emit
const { emit } = defineEmits(['toggle', 'remove']) as {
  (event: 'toggle', id: number): void;
  (event: 'remove', id: number): void;
};

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
