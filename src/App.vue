<script setup>
import { ref } from "vue";

const name = ref("John Doe");
const status = ref("active");
const tasks = ref(["Task One", "Task Two", "Task Three"]);
</script>

<template>
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
</template>

<style scoped>
* {
  margin-top: 20px;
}

.status{
 display: flex;
 margin: 20px;
}

.task{
  display: block;
  margin: 0 auto 2rem;
}
</style>
