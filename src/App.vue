<script setup>
import { ref,onMounted } from "vue";

const name = ref("John Doe");
const status = ref("active");
const tasks = ref();
const newTask = ref('')

const addTask = () => {
  if(newTask.value.trim() !== ''){
    tasks.value.push(newTask.value)
    newTask.value = ''
  }
}

const deleteTask = (index) => {
  tasks.value.splice(index,1)
}

const toggleStatus = () => {
  if (status.value === "active") {
    status.value = "pending";
  } else if (status.value === "pending") {
    status.value = "inactive";
  } else {
    status.value = "active";
  }
};

onMounted( async () => {
  try{
    const response = await fetch('https://jsonplaceholder.typicode.com/todos')
    const data = await response.json()
    tasks.value = data.map((task) => task.title)
  } catch (error){
    console.log(error)
  }
})
</script>

<template>
  <div class="container">
    <h1>Hello {{ name }}</h1>

    <div class="status">
      <p v-if="status === 'active'">User is active</p>
      <p v-else-if="status === 'pending'">User is pending</p>
      <p v-else>User is inactive</p>
    </div>

    <form @submit.prevent="addTask">
      <label for="newTask">Add Task</label>
      <input type="text" name="newTask" v-model="newTask">
      <button type="submit">Submit</button>
    </form>

    <div class="task">
      <h1>Tasks</h1>
      <ul>
        <li v-for="(task,index) in tasks" :key="task">
          <span> {{ task }} </span> 
          <button @click="deleteTask(index)">X</button>
        </li>
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
