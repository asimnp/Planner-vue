<script setup>
import { ref } from "vue";

const tasks = ref([
  { id: 1, text: "Read book", done: true },
  { id: 2, text: "Complete homework", done: false },
  { id: 3, text: "Plane day", done: true },
]);
</script>

<template>
  <h1>Planner!</h1>
  <h3>Tasks</h3>
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
