<script>
export default {
  data() {
    return {
      name: 'John Doe',
      status: 'active',
      tasks: [
        { id: 1, title: 'Task 1', isCompleted: true },
        { id: 2, title: 'Task 2', isCompleted: false },
        { id: 3, title: 'Task 3', isCompleted: true },
      ],
      link: 'https://www.google.com'
    };
  },
  methods: {
    toggleStatus() {
      this.status = this.status === 'active' ? 'pending' : 'active';
    },
  },
};
</script>

<template>
  <h1>{{ name }}</h1>
  <p v-if="status === 'active'">User is {{status}}!</p>
  <p v-else-if="status === 'pending'">User is {{status}}!</p>
  <p v-else>User is not active!</p>

  <h3>Tasks</h3>
  <ul>
    <li v-for="task in tasks" :key="task.id">
      {{ task.title }}
    </li>
  </ul>
  <!-- <a v-bind:href="link">Google</a> -->
  <a :href="link">Google</a>
  <br>
  <!-- <button v-on:click="toggleStatus = 'active'">Activate</button> -->
  <button v-on:click="toggleStatus">Change Status</button>
</template>
