<template>
  <div class="todo-input-form">
    <input
      v-model="text"
      @keyup.enter="handleSubmit"
      placeholder="Add todo..."
    />
    <button @click="handleSubmit">Add</button>
  </div>
</template>

<script setup>
import { ref, defineEmits } from "vue";

const text = ref("");
const emit = defineEmits(["addTodo"]);

const handleSubmit = () => {
  if (text.value.trim()) {
    const updateStartTime = performance.now();
    emit("addTodo", text.value.trim(), updateStartTime);
    text.value = "";
  }
};
</script>

<style scoped>
.todo-input-form {
  display: flex;
  justify-content: center;
  margin: 20px 0;
}
</style>
