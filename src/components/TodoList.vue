<template>
    <div class="todo-list-container">
        <form @submit.prevent="updateTask" action="" class="todo-form">
            <input v-model="newTask" type="text" placeholder="Ведите новую задачу" class="todo-input">
            <button type="submit" class="todo-btn">
                Добавить
            </button>
        </form>
        <ul class="todo-list">
            <TodoItem
            v-for="task in tasks"
            :key="task.id"
            :task="task"
            @remove-task="$emit('remove-task', $event)"
            @toggle-status="$emit('toggle-status', $event)"
            />
        </ul>
    </div>
</template>
<!-- v-model делает связь между input и введенным значением, значение автоматически сохраняется -->
<!-- @submit.prevent="updateTask" запускает функцию updateTask -->
<script>
import { ref } from 'vue';
import TodoItem from './TodoItem.vue';

export default {
    name: "ToDoList",
    emits: ['add-task', 'remove-task', 'toggle-status'],
    props: ['tasks'],
    components: { TodoItem },

    setup(_, {emit}) {
        const newTask = ref('');

        // обновляем строку чтобы она стала пустой
        const updateTask = () => {
            if(newTask.value.trim()){
                emit('add-task', newTask.value.trim())
                newTask.value = '';
            }
        }

        return { newTask, updateTask};
    },
};


</script>

  <style scoped>

  .todo-list-container {
    background: #fff;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  }
  
  .todo-form {
    display: flex;
    gap: 10px;
    margin-bottom: 20px;
  }
  
  .todo-input {
    flex: 1;
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 4px;
  }
  
  .todo-btn {
    background-color: #4caf50;
    color: white;
    border: none;
    padding: 10px 20px;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.3s;
  }
  
  .todo-btn:hover {
    background-color: #45a049;
  }
  
  .todo-list {
    list-style: none;
    padding: 0;
  }
</style>