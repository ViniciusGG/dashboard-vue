<script setup>
import { onMounted, ref } from 'vue';

    const name = ref('John Doe');
    const status = ref('active');
    const tasks = ref([
      { id: 1, title: 'Task 1', isCompleted: true },
      { id: 2, title: 'Task 2', isCompleted: false },
      { id: 3, title: 'Task 3', isCompleted: true },
    ]);
    const newTask = ref('');

    const toggleStatus = () => {
      status.value = status.value === 'active' ? 'pending' : 'active';
    };

    const addTask = (e) => {
      if(!newTask.value) return;
      e.preventDefault();
      tasks.value.push({ id: tasks.value.length + 1, title: newTask.value, isCompleted: false });
      newTask.value = '';
    };

    const deleteTask = (task) => {
      tasks.value.splice(tasks.value.indexOf(task), 1);
    };

    onMounted(async () => {
      try {
        const response = await fetch('https://jsonplaceholder.typicode.com/todos');
        const data = await response.json();
        tasks.value = data.map((task) => ({ id: task.id, title: task.title, isCompleted: task.completed }));
      } catch (error) {
        console.error(error);
      }
    });

</script>

<template>
  <h1>{{ name }}</h1>
  <p v-if="status === 'active'">User is {{status}}!</p>
  <p v-else-if="status === 'pending'">User is {{status}}!</p>
  <p v-else>User is not active!</p>

  <form @submit.prevent="addTask">
    <input type="text" v-model="newTask" />
    <button>Add Task</button>
  </form>

  <h3>Tasks</h3>
  <ul>
    <li v-for="task in tasks" :key="task.id">
      <span>{{ task.title }}</span> <button @click="task.isCompleted = !task.isCompleted">{{ task.isCompleted ? 'Completed' : 'Not Completed' }}</button> <button @click="deleteTask(task)">Delete</button>
    </li>
  </ul>
  <br>
  <!-- <button v-on:click="toggleStatus = 'active'">Activate</button> -->
  <button v-on:click="toggleStatus">Change Status</button>
</template>
