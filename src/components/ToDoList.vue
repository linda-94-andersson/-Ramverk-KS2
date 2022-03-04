<script setup>
import { ref } from "vue";

let idKey = 0;

const newItem = ref("");
const todos = ref([{ id: idKey++, text: "Add new tasks" }]);

function addTodo() {
  todos.value.push({ id: idKey++, text: newItem.value });
  newItem.value = "";
}

function removeTodo(todo) {
  todos.value = todos.value.filter((target) => target !== todo);
}
</script>

<template>
  <form v-on:submit.prevent="addTodo">
    <input v-model="newItem" @keyup.enter="addTodo" type="text" />
    <button @click="addTodo" type="submit">Add todo</button>
  </form>
  <ul>
    <li v-for="todo in todos" :key="todo.id">
      {{ todo.text }}
      <button @click="removeTodo(todo)">X</button>
    </li>
  </ul>
</template>

<style></style>
