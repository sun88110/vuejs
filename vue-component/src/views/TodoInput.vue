<template>
  <slot name="header"></slot>
  <div>
    <input
      type="text"
      placeholder="새 할일을 입력하세요"
      v-model="newWork"
      v-on:change="addHandle"
    /><!--v-on:keyup.enter="addHandle" 이라고하면 엔터가 눌렷다가 때질때 함수실행-->
    <button v-on:click="AddHandle">추가</button>
  </div>
  <slot></slot>
  <slot name="footer"></slot>
</template>

<script setup>
import { ref, inject } from 'vue';

const newWork = ref('초기값');
const addHandle = inject('addTodo');

const AddHandle = () => {
  addHandle(newWork.value);
};
</script>
