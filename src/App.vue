<script setup>
import { ref } from "vue";

const name = ref("John Doe");
const status = ref("active");
const tasks = ref(["Task One", "Task Two", "Task Three"]);

const toggleStatus = () => {
  if (status.value === "active") {
    status.value = "pending";
  } else if (status.value === "pending") {
    status.value = "inactive";
  } else {
    status.value = "active";
  }
};
</script>

<template>
  <div class="container">
    <h1>Hello {{ name }}</h1>

    <div class="status">
      <p v-if="status === 'active'">User is active</p>
      <p v-else-if="status === 'pending'">User is pending</p>
      <p v-else>User is inactive</p>
    </div>

    <div class="task">
      <h1>Tasks</h1>
      <ul>
        <li v-for="task in tasks" :key="task">{{ task }}</li>
      </ul>
    </div>

    <button @click="toggleStatus">Change Status</button>
  </div>
</template>

<style scoped>
.task {
  display: block;
  margin: 20px;
}
</style>
