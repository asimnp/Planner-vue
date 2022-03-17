<script setup>
import { ref } from "vue";
import { v4 as uuidv4 } from "uuid";

const newTask = ref("");
const tasks = ref([]);

function addTask() {
  const task = { id: uuidv4(), text: newTask.value, done: false };
  tasks.value.push(task);
  newTask.value = "";
}
</script>

<template>
  <h1>Planner!</h1>
  <h3>Tasks</h3>

  <form @submit.prevent="addTask">
    <input type="text" v-model="newTask" />
    <button type="submit">Add Task</button>
  </form>

  <ul v-if="tasks.length">
    <li v-for="task in tasks" :key="task.id">
      <input type="checkbox" :id="task.id" v-model="task.done" />
      <label :for="task.id">{{ task.text }}</label>
      <button class="remove-btn">X</button>
    </li>
  </ul>
  <p v-else>No tasks added yet.</p>
</template>

<style>
.remove-btn {
  margin-left: 1em;
}
</style>
