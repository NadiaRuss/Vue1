<template>
  <div class="app-container">
      <h1 class="title">To-do List Vue3</h1>
      <ToDoList
      :tasks="tasks"
      @add-task = "addTask"
      @remove-task="removeTask"
      @toggle-status="toggleTaskStatus"
      />
  </div>

</template>


<script>

  import { ref } from 'vue';
  import ToDoList from './components/toDoList.vue';

  export default {
    name: "App",
    components: { ToDoList },
// создаем переменную, где будем хранить ввчеденные task, перед этим импортируем ref
   setup() {
    const tasks = ref([]);

    // создаем функцию которая будет менять список задач
    const addTask = (task) => {
      tasks.value.push({
        id: Date.now(),
        text: task,
        completed: false,
      })
    };
    const removeTask = (taskId) => {
      tasks.value = tasks.value.filter((task) => task.id != taskId)
    }

    const toggleTaskStatus = (task) => {
      task.completed = !task.completed;
    }
    return { tasks, addTask, removeTask, toggleTaskStatus };
   }
}
</script>

<style scoped>
.app-container {
  font-family: Arial, Helvetica, sans-serif;
  text-align: center;
  background-color: #f5f5f5;
  padding: 20px;
  border-radius: 10px;
  max-width: 600px;
  margin: 40px auto;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}
.title {
  font-size: 2.5rem;
  color: #333;
  margin-bottom: 20px;
}

</style>