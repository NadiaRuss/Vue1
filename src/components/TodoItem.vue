<template>
    <li :class="{ completed: task.completed}" class="todo-item">
        <span @click="$emit('toggle-status', task)" class="task-text">
            {{ task.text }}
        </span>
        <button @click="$emit('remove-task', task.id)" class="delete-btn">Удалить</button>
    </li>
</template>


<script>
export default {
    name: 'TodoItem',
    props: ['task'],
    emits: ['toggle-status', 'remove-task']
}

</script>


<style scoped>
.todo-item {
  display: flex;
  justify-content: space-between;
  padding: 10px;
  border-bottom: 1px solid #ddd;
}

.completed .task-text {
  text-decoration: line-through;
  color: #aaa;
}

.task-text {
  cursor: pointer;
  flex: 1;
}

.delete-btn {
  background-color: #f44336;
  color: white;
  border: none;
  border-radius: 4px;
  padding: 5px 10px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.delete-btn:hover {
  background-color: #e53935;
}
</style>