<template>
  <div :class="darkMode ? 'todo-container dark' : 'todo-container'">
    <header class="todo-header">
      <h1 class="todo-title">Todo List</h1>
      <time>{{ localDate }} - {{ localTime }}</time>
      <button @click="darkModeActive">Dark mode</button>
    </header>
    <AddTodo @add-todo="addTodo" ></AddTodo>
    <TodoList :todos="todos" @todo-remove="removeTodo" v-if="todos.length" :darkMode="darkMode"></TodoList>
    <p v-else class="todos-empty">Empty List</p>
  </div>
</template>

<script>
import { ref } from "vue";
import TodoList from './components/TodoList.vue';
import AddTodo from "./components/AddTodo.vue";

export default {
  name: 'App',
  components: {
    TodoList,
    AddTodo
  },
  setup() {
    const todos = ref([]);
    const darkMode = ref(false);
    const localDate = new Date().toLocaleDateString();
    const localTime = new Date().toLocaleTimeString();

    function getTodos() {
      const data = localStorage.getItem('todos');
      data ? todos.value = JSON.parse(data) : null;
    }
    getTodos();

    function removeTodo(id) {
      todos.value = todos.value.filter(todo => todo.id !== id);
      localStorage.setItem('todos', JSON.stringify(todos.value));
    }

    function addTodo(todo) {
      todos.value.push(todo);
      localStorage.setItem('todos', JSON.stringify(todos.value));
    }
    function darkModeActive() {
      darkMode.value ? darkMode.value = false : darkMode.value = true;
    }

    return {
      todos,
      removeTodo,
      addTodo,
      getTodos,
      localDate,
      localTime,
      darkMode,
      darkModeActive
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  text-decoration: none;
  box-sizing: border-box;
  list-style: none;
}

.todo-container {
  width: 900px;
  margin: auto;
  margin-top: 50px;
  border: 2px solid blue;
  padding: 20px;
}

.todo-container.dark {
  background: black;
  color: white;
}

.todos-empty {
  margin-top: 20px;
}

.todo-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>
