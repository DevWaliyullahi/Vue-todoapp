<template>
  <div class="container">
    <div class="input-container">
      <input type="text" v-model="newTask" placeholder="Add a new task" @keyup.enter="addTask">
      <button @click="addTask">Add</button>
    </div>
    <ul>
      <li v-for="(todo, index) in todos" :key="index">
        <div :class="{ 'completed': todo.completed }">
          <span>{{ todo.text }}</span>
          <div class="actions">
            <button @click="toggleCompletion(index)">
              {{ todo.completed ? 'Mark Incomplete' : 'Mark Completed' }}
            </button>
            <button @click="editTask(index)">Edit</button>
            <button @click="removeTodo(index)">Remove</button>
          </div>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
import { defineComponent, ref, watch } from 'vue';
import TodoItem from './TodoItem.vue';

export default defineComponent({
  components: {
    TodoItem,
  },
  setup() {
    const newTask = ref('');
    const todos = ref(JSON.parse(localStorage.getItem('todos')) || []);

    const addTask = () => {
      if (newTask.value.trim() !== '') {
        todos.value.push({ text: newTask.value, completed: false });
        newTask.value = '';
        localStorage.setItem('todos', JSON.stringify(todos.value));
      }
    };

    const removeTodo = (index) => {
      todos.value.splice(index, 1);
      localStorage.setItem('todos', JSON.stringify(todos.value));
    };

    const editTask = (index) => {
      const newText = prompt('Edit task:', todos.value[index].text)
      if (newText !== null) {
        todos.value[index].text = newText;
        localStorage.setItem('todos', JSON.stringify(todos.value));
      }
    };

    const toggleCompletion = (index) => {
      todos.value[index].completed = !todos.value[index].completed;
      localStorage.setItem('todos', JSON.stringify(todos.value));
    };

    // Watch todos for changes and store in local storage
    watch(todos, (newVal) => {
      localStorage.setItem('todos', JSON.stringify(newVal));
    });

    return {
      newTask,
      todos,
      addTask,
      removeTodo,
      editTask,
      toggleCompletion,
    };
  },
});
</script>

<style scoped>
.container {
  margin-top: 20px;
}

.input-container {
  display: flex;
  align-items: center;
  margin-bottom: 10px;
}

.input-container input[type="text"] {
  flex: 1;
  padding: 10px;
  font-size: 16px;
}

.input-container button {
  padding: 10px;
  font-size: 16px;
  background-color: #202122;
  color: #fff; 
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

ul {
  list-style: none;
  padding: 0;
}

.completed {
  text-decoration: line-through;
}

.actions {
  display: flex;
}

.actions button {
  margin-right: 5px;
}
</style>

