<script setup>
import { ref } from "vue";

const name = ref("John Doe");
const status = ref("active");
const tasks = ref(["Task One", "Task Two", "Task Three"]);
</script>

<template>
  <h1>Hello {{ name }}</h1>

  <p v-if="status === 'active'">User is active</p>
  <p v-else-if="status === 'pending'">User is pending</p>
  <p v-else>User is inactive</p>

  <h1>Tasks</h1>
  <ul>
    <li v-for="task in tasks" :key="task"> {{ task }}</li>
  </ul>
</template>
