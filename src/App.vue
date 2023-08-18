<template>
  <div class="app">
    <div class="input-container">
      <h2>To Do List</h2>
      <input v-model="newTask.text" type="text" placeholder="輸入記事" @keydown="handleInputKeydown" />
      <input v-model="newTask.date" type="date">
      <input v-model="newTask.time" type="time">
      <button @click="addTask">新增</button>
    </div>
    <div class="task-list">
      <div class="task-item" v-for="(task, index) in tasks" :key="index">
        <TodoItem :task="task" @delete="deleteTask(index)" />
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import TodoItem from './components/TodoItem.vue';

interface Task {
  text: string;
  completed: boolean;
  date: string;
  time: string;
}

const newTask = ref<Task>({
  text: '',
  completed: false,
  date: '',
  time: ''
});
const tasks = ref<Task[]>([]);

const addTask = () => {
  if (newTask.value.text.trim() !== '') {
    tasks.value.push({ ...newTask.value });
    newTask.value = { text: '', completed: false, date: '', time: '' };
  }
};

const deleteTask = (index: number) => {
  tasks.value.splice(index, 1);
};

const handleInputKeydown = (event: KeyboardEvent) => {
  if (event.key === 'Enter') {
    addTask();
  }
};
</script>