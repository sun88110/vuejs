<template>
  <li v-bind:class="{ completed: todo.complted }">
    <span v-on:click="handleToggle">{{ todo.text }}</span>
    <TodoItemButton v-bine:item-id="todo.id" />
  </li>
</template>

<script setup>
import { defineProps, inject } from 'vue'; //todo 데이터값 받아오기
import TodoItemButton from './TodoitemButton.vue';
//inject <- props와
const toggleComplete = inject('toggleComplete');
//props <-얘는 데이터 받아오는거
const props = defineProps({
  todo: { type: Object, required: true },
});

//함수.
const handleToggle = () => {
  toggleComplete(props.todo.id);
};
</script>

<style scoped>
.completed span {
  text-decoration: line-through;
  color: gray;
}
</style>
