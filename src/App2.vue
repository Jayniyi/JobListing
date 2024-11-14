<script setup>
import { ref, onMounted } from "vue";

const name = ref("john doe");
const status = ref("active");
const tasks = ref(["task one", "task two", "task three"]);
const newTask = ref("");
const toggleStatus = () => {
  if (status.value === "active") {
    status.value = "pending";
  } else if (status.value === "pending") {
    status.value = "inactive";
  } else {
    status.value = "active";
  }
};

const addTask = () => {
  if (newTask.value.trim() !== "") {
    tasks.value.push(newTask.value);
    newTask.value = "";
  }
};
const deleteTask = (index) =>{
  tasks.value.splice(index,1)
};

onMounted(async () => {
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/todos');
  const data =  await response.json();
  tasks.value =  data.map((task) => task.title);
  } catch (error) {
console.log('error fetching task');
  }
});
</script>
<template>
  <h2>{{ name }}</h2>
  <p v-if="status === 'active'">user is active</p>
  <p v-else-if="status === 'pending'">user is pending</p>
  <p v-else>user is inactive</p>
  <form @submit.prevent="addTask">
    <label for="newwtask">Add TASK</label>
    <input type="text" id="newTask" name=" newTask" v-model="newTask" />
    <button type="submit">submit</button>
  </form>
  <h3>Task</h3>
  <ul>
    <li v-for="(task, index) in tasks" :key="task">
      <span> {{ task }}</span>
      <button @click="deleteTask(index)">x</button>
    </li>
  </ul>
  <button @click="toggleStatus">change status</button>
</template>
<!-- <script setup>
import { ref, onMounted } from "vue";

const name = ref("john doe");
const status = ref("active");
const tasks = ref(["task one", "task two", "task three"]);
const newTask = ref("");
const toggleStatus = () => {
  if (status.value === "active") {
    status.value = "pending";
  } else if (status.value === "pending") {
    status.value = "inactive";
  } else {
    status.value = "active";
  }
};

const addTask = () => {
  if (newTask.value.trim() !== "") {
    tasks.value.push(newTask.value);
    newTask.value = "";
  }
};
const deleteTask = (index) =>{
  tasks.value.splice(index,1)
};

onMounted(async () => {
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/todos');
  const data =  await response.json();
  tasks.value =  data.map((task) => task.title);
  } catch (error) {
console.log('error fetching task');
  }
});
</script>
<template>
  <h2>{{ name }}</h2>
  <p v-if="status === 'active'">user is active</p>
  <p v-else-if="status === 'pending'">user is pending</p>
  <p v-else>user is inactive</p>
  <form @submit.prevent="addTask">
    <label for="newwtask">Add TASK</label>
    <input type="text" id="newTask" name=" newTask" v-model="newTask" />
    <button type="submit">submit</button>
  </form>
  <h3>Task</h3>
  <ul>
    <li v-for="(task, index) in tasks" :key="task">
      <span> {{ task }}</span>
      <button @click="deleteTask(index)">x</button>
    </li>
  </ul>
  <button @click="toggleStatus">change status</button>
</template> -->
