<template>
  <div id="app" class="App">
    <AppHeader />
    <div className="todo-info">
      <p>Total Todos: {{ todos.length }}</p>
      <p>Completed: {{ completedCount }}</p>
    </div>
    <TodoInput @addTodo="addTodo" />
    <TodoList
      :todos="todos"
      @toggleTodo="toggleTodo"
      @deleteTodo="deleteTodo"
    />
    <button class="reset-button" @click="resetTodos">Reset Todos</button>
  </div>
</template>

<script setup>
import { ref, onMounted, onUpdated, nextTick } from "vue";
import AppHeader from "./components/AppHeader.vue";
import TodoInput from "./components/TodoInput.vue";
import TodoList from "./components/TodoList.vue";

const startTime = performance.now();

const todos = ref([]);
const completedCount = ref(0);

onMounted(() => {
  const endTime = performance.now();
  const renderTime = endTime - startTime;
  console.log(`Initial render time: ${renderTime.toFixed(2)} milliseconds.`);
});

onUpdated(() => {}, [todos]);

const addTodo = (text, updateStartTime) => {
  todos.value.push({ id: Date.now(), text, completed: false });
  nextTick(() => {
    const endTime = performance.now();
    const renderTime = endTime - updateStartTime;
    console.log(`Update time: ${renderTime.toFixed(2)} milliseconds.`);
  });
};

const toggleTodo = (id, updateStartTime) => {
  const todo = todos.value.find((t) => t.id === id);
  if (todo) {
    todo.completed = !todo.completed;
    completedCount.value = todos.value.filter((t) => t.completed).length;
  }
  nextTick(() => {
    const endTime = performance.now();
    const renderTime = endTime - updateStartTime;
    console.log(`Update time: ${renderTime.toFixed(2)} milliseconds.`);
  });
};

const deleteTodo = (id, updateStartTime) => {
  todos.value = todos.value.filter((t) => t.id !== id);
  completedCount.value = todos.value.filter((t) => t.completed).length;
  nextTick(() => {
    const endTime = performance.now();
    const renderTime = endTime - updateStartTime;
    console.log(`Update time: ${renderTime.toFixed(2)} milliseconds.`);
  });
};

const resetTodos = () => {
  const updateStartTime = performance.now();
  todos.value = [];
  completedCount.value = 0;
  nextTick(() => {
    const endTime = performance.now();
    const renderTime = endTime - updateStartTime;
    console.log(`Update time: ${renderTime.toFixed(2)} milliseconds.`);
  });
};
</script>

<style>
.App {
  text-align: center;
}

.todo-info {
  margin: 20px;
}

.reset-button {
  background-color: red;
  color: white;
  padding: 10px;
  border: none;
  cursor: pointer;
}

.todo-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  border: 1px solid #ccc;
  margin: 10px;
}

.completed {
  text-decoration: line-through;
}
</style>
