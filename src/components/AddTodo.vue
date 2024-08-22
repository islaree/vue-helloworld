<script setup>
import { ref } from "vue";
import { v4 as uuidv4 } from "uuid";

const emit = defineEmits(["add-todo"]);

const text = ref("");

const handleSubmit = (e) => {
  e.preventDefault();
  if (text.value.trim()) {
    emit("add-todo", { id: uuidv4(), text: text.value, completed: false });
  }
  text.value = "";
};
</script>

<template>
  <form class="flex" @submit="handleSubmit">
    <label>
      <input class="input" v-model="text" placeholder="todo name" />
    </label>
    <button>add todo</button>
  </form>
</template>

<style>
.flex {
  display: flex;
  align-items: center;
  gap: 8px;
}

.input {
  padding: 2px 6px;
  font-size: 16px;
}
</style>
