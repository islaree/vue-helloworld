<script setup>
import { ref } from "vue";
import AddTodo from "./AddTodo.vue";
import Todo from "./Todo.vue";

const todos = ref([]);

const addTodo = (newTodo) => {
  todos.value.unshift(newTodo);
};

const deleteTodo = (id) => {
  todos.value = todos.value.filter((todo) => todo.id !== id);
};

const editTodo = (id, newTodoText) => {
  todos.value = todos.value.map((todo) => {
    if (todo.id == id) {
      return { ...todo, text: newTodoText };
    }
    return todo;
  });
};
</script>

<template>
  <AddTodo @add-todo="addTodo" />
  <ul class="todo-list">
    <Todo
      v-for="todo in todos"
      :key="todo.id"
      :id="todo.id"
      :text="todo.text"
      :completed="todo.completed"
      @update:completed="todo.completed = $event"
      @delete-todo="deleteTodo"
      @edit-todo="editTodo"
    />
  </ul>
</template>

<style>
.todo-list {
  display: flex;
  flex-direction: column;
  gap: 8px;
  margin-top: 24px;
}
</style>
