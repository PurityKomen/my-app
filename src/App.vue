<script setup>
import { ref, onMounted } from "vue";

const name = ref("John Doe");
const status = ref("active");
const tasks = ref();
const newTask = ref("");

const addTask = () => {
  if (newTask.value.trim() !== "") {
    tasks.value.push(newTask.value);
    newTask.value = "";
  }
};

const deleteTask = (index) => {
  tasks.value.splice(index, 1);
};

const toggleStatus = () => {
  if (status.value === "active") {
    status.value = "pending";
  } else if (status.value === "pending") {
    status.value = "inactive";
  } else {
    status.value = "active";
  }
};

onMounted(async () => {
  try {
    const response = await fetch("https://jsonplaceholder.typicode.com/todos");
    const data = await response.json();
    tasks.value = data.map((task) => task.title);
  } catch (error) {
    console.log("error");
  }
});
</script>

<template>
  <div class="container-xl lg:container m-auto mt-3">
    <h1 class="text-2xl">Hello, {{ name }}</h1>

    <div class="status">
      <p v-if="status === 'active'">User is active</p>
      <p v-else-if="status === 'pending'">User is pending</p>
      <p v-else>User is inactive</p>
    </div>
    <button class="flex justify-center rounded-md bg-indigo-600 px-3 py-1.5 text-sm/6 font-semibold text-white shadow-xs hover:bg-indigo-500 focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600" @click="toggleStatus">Change Status</button>

    <div class="sm:mx-auto sm:w-full sm:max-w-sm">
      <form @submit.prevent="addTask">
        <div class="relative z-0 w-full mb-5 group">
          <label
            for="newTask"
            class="block text-sm/6 font-medium text-black-900"
            >Add Task</label
          >
          <input
            type="text"
            name="newTask"
            v-model="newTask"
            className="form-control p-2 mr-2 border-black  border-solid border-2 rounded-2xl focus:outline-none placeholder:text-black "
          />
        </div>
        <button
          class="flex justify-center rounded-md bg-indigo-600 px-3 py-1.5 text-sm/6 font-semibold text-white shadow-xs hover:bg-indigo-500 focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
          type="submit"
        >
          Submit
        </button>
      </form>
    </div>

    <div class="task">
      <h1 class="text-4xl">Tasks</h1>
      <ul class="list-disc">
        <li v-for="(task, index) in tasks" :key="task">
          <span> {{ task }} </span>
          <button
            @click="deleteTask(index)"
            class="m-2 border-4 border-black-500/50"
          >
            X
          </button>
        </li>
      </ul>
    </div>
  </div>
</template>

<style scoped>
.task {
  display: block;
  margin: 20px;
}
</style>
