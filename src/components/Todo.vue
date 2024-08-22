<script setup>
import { ref } from "vue";

const props = defineProps({
  id: String,
  text: String,
  completed: Boolean,
});

const isEditing = ref(false);
const newTodoText = ref(props.text);

const emit = defineEmits(["update:completed", "delete-todo", "edit-todo"]);

const onChange = (e) => {
  emit("update:completed", e.target.checked);
};

const handleDelete = () => {
  emit("delete-todo", props.id);
};

const handleSave = () => {
  emit("edit-todo", props.id, newTodoText.value);

  isEditing.value = false;
};
</script>

<template>
  <li class="flex">
    <input type="checkbox" :checked="completed" @change="onChange" />
    <div class="flex" v-if="isEditing">
      <input v-model="newTodoText" />
      <button @click="handleSave">save</button>
      <button @click="isEditing = false">cancel</button>
    </div>
    <div class="flex" v-else>
      <div :class="['todo-text', { completed: completed }]">
        {{ text }}
      </div>
      <button @click="isEditing = true">edit</button>
      <button @click="handleDelete">delete</button>
    </div>
  </li>
</template>

<style>
.flex {
  display: flex;
  align-items: center;
  gap: 10px;
}

.todo-text {
  font-size: 14px;
  color: black;
  text-decoration: none;
}

.todo-text.completed {
  color: gray;
  text-decoration: line-through;
}
</style>
