<template>
  <ul class="todo-list">
    <TodoItem
      v-for="todo in props.todos"
      :key="todo.id"
      :todo="todo"
      @toggleTodo="toggleTodo"
      @deleteTodo="deleteTodo"
    />
  </ul>
</template>

<script setup>
import { defineProps, defineEmits } from "vue";
import TodoItem from "./TodoItem.vue";

const props = defineProps({
  todos: {
    type: Array,
    required: false,
  },
});

const emit = defineEmits(["toggleTodo, deleteTodo"]);

const toggleTodo = (id, updateStartTime) => {
  emit("toggleTodo", id, updateStartTime);
};

const deleteTodo = (id, updateStartTime) => {
  emit("deleteTodo", id, updateStartTime);
};
</script>

<style scoped>
.todo-list {
  list-style-type: none;
  padding: 0;
}
</style>
