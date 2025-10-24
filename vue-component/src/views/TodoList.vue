<template>
  <h3>Todo List(Provide/Inject)</h3>
  <TodoInput>
    <template v-slot:header>
      <!--이렇게 템플릿 안에 템플릿을 선언하면 전달하는 데이터로 간주한다-->
      <h3>글등록header</h3>
    </template>
    <template v-slot:footer>
      <!--이렇게 템플릿 안에 템플릿을 선언하면 전달하는 데이터로 간주한다-->
      <h3>글등록footer</h3>
    </template>
    <template v-slot:default>
      <!--이렇게 템플릿 안에 템플릿을 선언하면 전달하는 데이터로 간주한다-->
      <h3>글등록slot</h3>
    </template>
  </TodoInput>
  <ul>
    <TodoItemContainer
      v-for="todo in todos"
      v-bind:key="todo.id"
      v-bind:todo="todo"
    ></TodoItemContainer>
  </ul>
</template>

<script setup>
import { reactive, provide } from 'vue';
import TodoInput from './TodoInput.vue';
import TodoItemContainer from './TodoItemContainer.vue';

// 데이터.
let nextId = 3;
const todoData = [
  { id: 1, text: 'Vue.js 이해하기', complted: false },
  { id: 2, text: 'Provied/Inject 처리 이해하기', complted: true },
];
const todos = reactive(todoData);
// 함수.
const addTodo = (newText) => {
  if (newText.trim() == '') return;
  todos.push({ id: nextId++, text: newText, complted: false });
};
const toggleComplete = (id) => {
  const todo = todos.find((t) => t.id == id);
  if (todo) {
    todo.complted = !todo.complted;
  }
};
const removeTodo = (id) => {
  const idx = todos.findIndex((t) => t.id == id);
  todos.splice(idx, 1);
};

//provides.. <- exports ????
provide('todos', todos);
provide('addTodo', addTodo);
provide('toggleComplete', toggleComplete);
provide('removeTodo', removeTodo);
</script>
