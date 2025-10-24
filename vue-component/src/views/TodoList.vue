<template>
  <h3>Todo List(Provide/Inject)</h3>
  <TodoInput />
  <ul>
    <TodoItemContainer />
  </ul>
</template>

<script setup>
import { reative, provide } from 'vue';
import TodoInput from './TodoInput.vue';
import TodoItemContainer from './TodoItemContainer.vue';

// 데이터.
const todoData = [
  { id: 1, text: 'Vue.js 이해하기', complted: false },
  { id: 2, text: 'Provied/Inject 처리 이해하기', complted: true },
];
const todos = reative(todoData);

//provides..
provide('todos', todos);
</script>
