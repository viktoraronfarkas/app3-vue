<template>
  <li class="todo-item">
    <span :class="{ completed: props.todo.completed }">{{
      props.todo.text
    }}</span>
    <button class="toggle-button" @click="toggleTodo(props.todo.id)">
      {{ props.todo.completed ? "Unmark" : "Complete" }}
    </button>
    <button class="delete-button" @click="deleteTodo(props.todo.id)">
      Delete
    </button>
  </li>
</template>

<script setup>
import { defineProps, defineEmits } from "vue";

const props = defineProps({
  todo: {
    id: {
      type: Number,
      required: false,
    },
    text: {
      type: String,
      required: false,
    },
    completed: {
      type: Boolean,
      required: false,
    },
  },
});
const emit = defineEmits(["toggleTodo", "deleteTodo"]);

const toggleTodo = (id) => {
  const updateStartTime = performance.now();
  emit("toggleTodo", id, updateStartTime);
};

const deleteTodo = (id) => {
  const updateStartTime = performance.now();
  emit("deleteTodo", id, updateStartTime);
};
</script>

<style scoped>
.completed {
  text-decoration: line-through;
}

.toggle-button {
  background-color: green;
  color: white;
  padding: 5px;
  border: none;
  cursor: pointer;
}

.delete-button {
  background-color: red;
  color: white;
  padding: 5px;
  border: none;
  cursor: pointer;
}
</style>
