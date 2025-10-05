<script setup>
import { onMounted, ref } from 'vue';

  const name = ref('John Doe');
  const status = ref('active');
  const tasks = ref(['Task 1', 'Task 2', 'Task 3']);
  const newTask = ref('');    
  const ToggleEvent = () => {
    status.value = status.value === 'active' ? 'inactive' : 'active';
    console.log('Chnaged Status');
};

  const addTask = () => {
    if (newTask.value.trim() !== '') {
    tasks.value.push(newTask.value.trim());
    newTask.value = '';
    }
  };

  const deleteTask = (index) => {
    tasks.value.splice(index, 1);
  };

  onMounted(async() => {
    try {
      const response = await fetch('https://jsonplaceholder.typicode.com/todos');
      const data = await response.json();
      tasks.value = data.slice(index,1).map(item => item.title);
    } catch (error) {
      console.error('Error fetching tasks:', error);
    }
  });
     
</script>

<template>
  <h1>
    {{ name }}
  </h1>
  <p v-if="status === 'active'">
    Status is active  
  </p>
  <p v-else-if="status === 'inactive'">
    Status is inactive
  </p>
  <p v-else>
    Status is unknown
  </p>

  <form @submit.prevent="addTask">
    <label for="newTask">Add Task</label>
    <input type="text" id="newTask" name="newTask" v-model="newTask" />
    <button type="submit">Add</button>
  </form>

  <h3>
    Tasks:
  </h3>
    <ul>
      <li v-for="task in tasks" key="task">
        <span>

          {{ task }}
        </span>
        <button @click="deleteTask">X</button>
      </li>
    </ul>
    
    &nbsp;
    <button @click="ToggleEvent">Change Status</button>
</template>

