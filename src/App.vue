<script setup>
import { ref, computed } from "vue";
import { v4 as uuidv4 } from "uuid";

const newTask = ref("");
const tasks = ref([]);
const hideTasks = ref(false);

function addTask() {
  const task = { id: uuidv4(), text: newTask.value, done: false };
  tasks.value.push(task);
  newTask.value = "";
}

function removeTask(task) {
  tasks.value = tasks.value.filter((t) => t !== task);
}

const filteredTasks = computed(() => {
  return hideTasks.value ? tasks.value.filter((t) => !t.done) : tasks.value;
});
</script>

<template>
  <h1>Planner!</h1>
  <h3>Tasks</h3>

  <form @submit.prevent="addTask">
    <input type="text" v-model="newTask" />
    <button type="submit">Add Task</button>
  </form>

  <ul v-if="tasks.length">
    <li v-for="task in filteredTasks" :key="task.id">
      <input type="checkbox" :id="task.id" v-model="task.done" />
      <label :for="task.id">{{ task.text }}</label>
      <button class="remove-btn" @click="removeTask(task)">X</button>
    </li>
  </ul>
  <p v-else>No tasks added yet.</p>

  <button @click="hideTasks = !hideTasks" v-if="tasks.length">
    {{ hideTasks ? "Show all" : "Hide completed tasks" }}
  </button>
</template>

<style>
.remove-btn {
  margin-left: 1em;
}
</style>
