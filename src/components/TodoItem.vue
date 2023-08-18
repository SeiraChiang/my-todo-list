<template>
  <div class="task-line">
    <input type="checkbox" v-if="task" v-model="task.completed" />
    <div class="task-data">
      <input v-if="task" v-model="task.text" />
      <input v-if="task" v-model="task.date" type="date" />
      <input v-if="task" v-model="task.time" type="time" />
    </div>
    <button @click="deleteTask">刪除</button>
  </div>
</template>


<script setup lang="ts">

interface Task {
  text: string;
  completed: boolean;
  date: string;
  time: string;
}

const props = defineProps({
  task: Object as () => Task
});

const emit = defineEmits();

const deleteTask = () => {
  emit('delete', props.task);
};
</script>

<style>
.task-line {
  width: 100%;
  border-bottom: 1px solid #213547;
  margin-bottom: 10px;
  padding-bottom: 10px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.task-data input{
  display: block;
  margin-bottom: 5px;
}
</style>
  
  
  