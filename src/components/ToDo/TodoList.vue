<template>
    <h1>Lista de Tareas</h1>
    <input class="add-task" v-model="newTask" @keyup.enter="addTask" placeholder="Nueva tarea">
    <ul>
        <TodoItem v-for="(task, index) in tasks" :key="index" :task="task" 
            :deleteTask="() => deleteTask(index)" 
            :toggleTask="() => toggleTask(index)" />
    </ul>
</template>

<script setup>
import { ref, watchEffect } from 'vue';
import TodoItem from './TodoItem.vue';

const tasks = ref(JSON.parse(localStorage.getItem('tasks')) || []);
const newTask = ref('');

watchEffect(() => {
    localStorage.setItem('tasks', JSON.stringify(tasks.value));
});

const addTask = () => {
    if(newTask.value != ''){
        tasks.value.push({ text: newTask.value, completed: false });
        newTask.value = '';
    }
};

const deleteTask = (index) => {
    tasks.value.splice(index, 1);
};

const toggleTask = (index) => {
    tasks.value[index].completed = !tasks.value[index].completed;
};
</script>


<style scoped>
.add-task {
    width: 100%;
    max-width: 512px;
    padding: 10px;
    font-size: 16px;
    border-radius: 5px;
    border: 1px solid #ccc;
    margin-bottom: 1rem;
}

ul {
    width: 100%;
    max-width: 512px;
    padding: 0;
}
</style>
