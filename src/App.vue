<template>
  <div class="app-container">
    <h1>Vue 3 Todo App</h1>
    <form @submit.prevent="addNewTodo">
       <label for="newTodo">New todo</label>
       <input v-model="newTodo" id="newTodo" placeholder="Enter a new task">
       <button class="add-button">Add New Todo</button>
    </form>
    <div class="actions">
      <button @click="removeAllTodos" class="remove-all-button">REMOVE All</button>
      <button @click="markAllDone" class="mark-all-done-button">Mark All Done</button>
    </div>
    <ul class="todo-list">
      <li v-for="(todo, index) in todos" :key="todo.id" class="todo-item">
        <h3 :class="{ done: todo.done }" @click="toogleDone(todo)">{{ todo.content }}</h3>
        <button @click="removeTodo(index)" class="remove-button">Remove Todo</button>
      </li>
    </ul>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const newTodo = ref('');
    const todos = ref([]);

    function addNewTodo() {
      todos.value.push({
        id: Date.now(),
        done: false,
        content: newTodo.value,
      });
      newTodo.value = '';
    }

    function toogleDone(todo) {
      todo.done = !todo.done;
    }

    function removeTodo(index) {
      todos.value.splice(index, 1);
    }

    function markAllDone() {
      todos.value.forEach((todo) => (todo.done = true));
    }

    function removeAllTodos() {
      todos.value = [];
    }

    return {
      todos,
      newTodo,
      addNewTodo,
      toogleDone,
      removeTodo,
      markAllDone,
      removeAllTodos,
    };
  },
};
</script>

<style scoped>
.app-container {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  background-color: #f4f7f9;
  border-radius: 10px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  font-family: 'Arial', sans-serif;
}

h1 {
  color: #333;
  text-align: center;
  margin-bottom: 20px;
}

form {
  display: flex;
  justify-content: space-between;
  margin-bottom: 20px;
}

input {
  flex: 1;
  padding: 10px;
  border-radius: 5px;
  border: 1px solid #ccc;
  font-size: 16px;
}

input::placeholder {
  color: #aaa;
}

button {
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.add-button {
  background-color: #4caf50;
  color: white;
  margin-left: 10px;
}

.add-button:hover {
  background-color: #45a049;
}

.actions {
  display: flex;
  justify-content: space-between;
  margin-bottom: 20px;
}

.remove-all-button {
  background-color: #e74c3c;
  color: white;
}

.remove-all-button:hover {
  background-color: #c0392b;
}

.mark-all-done-button {
  background-color: #3498db;
  color: white;
}

.mark-all-done-button:hover {
  background-color: #2980b9;
}

.todo-list {
  list-style: none;
  padding: 0;
}

.todo-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: white;
  padding: 10px;
  border-radius: 5px;
  margin-bottom: 10px;
  box-shadow: 0 1px 5px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease;
}

.todo-item:hover {
  transform: translateY(-3px);
}

.todo-item h3 {
  margin: 0;
  flex: 1;
  cursor: pointer;
  transition: color 0.3s ease;
}

.todo-item h3.done {
  text-decoration: line-through;
  color: #bbb;
}

.remove-button {
  background-color: #e74c3c;
  color: white;
}

.remove-button:hover {
  background-color: #c0392b;
}
</style>
