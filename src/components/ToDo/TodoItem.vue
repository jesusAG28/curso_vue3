<template>
  <li :class="{ completed: task.completed }">
    <div class="task-text">
      {{ task.text }}
    </div>
    <div class="buttons">
      <button class="btn" @click="toggleTask" :class="{ 'btn-complete': !task.completed }">
        <Check v-if="!task.completed" />
        <Reopen v-else />
      </button>
      <button class="btn btn-delete" @click="deleteTask">
        <Trash />
      </button>
    </div>
  </li>
</template>

<script setup>
import { ref } from 'vue';
import Trash from '../Trash.vue';
import Check from '../Check.vue';
import Reopen from '../Reopen.vue';

const props = defineProps(['task', 'deleteTask', 'toggleTask']);
</script>

<style scoped>
.completed .task-text {
  text-decoration: line-through;
}

.buttons {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: flex-end;
  text-decoration: none;
}

.btn {
  margin-left: 10px;
  padding: 2px 4px;
  border: none;
  border-radius: 5px;
  background-color: #007BFF;
  color: white;
  cursor: pointer;
  text-decoration: none;
}

.btn:hover {
  background-color: #0056b3;
}

.completed .btn {
  text-decoration: none;
}

.btn-delete {
  background-color: #ff3434;
}

.btn-delete:hover {
  background-color: #ff7070;
}

.btn-complete {
  background-color: #35ae1d;
}

.btn-complete:hover {
  background-color: #91f27d;
}


li {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  border-radius: 5px;
  margin-bottom: .3rem;
}

li:hover {
  background-color: darkcyan;
}
</style>
