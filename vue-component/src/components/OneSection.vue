<script setup>
import { defineProps, defineEmits } from 'vue' //props는 상위에서 받을때 emits은 하위에서 보낼때

defineProps({
  title: {
    type: String,
    required: true,
  },
  content: {
    type: String,
    default: '안녕하세요',
  },
})
const emit = defineEmits(['callStarPoint']) //상위 컴포넌트 전달받기

const onClick = (e) => {
  console.log(e.target.parentElement.parentElement.children[1].innerText)

  emit('callStarPoint', e.target.parentElement.parentElement.children[0].innerText) // 전달받은 정의 이벤트를 송출받음
}
</script>

<template>
  <section class="box">
    <h3>{{ title }}</h3>
    <p>{{ content }}</p>
    <p><button v-on:click="onClick">복제된 인류말살버튼</button></p>
  </section>
</template>

<style scoped>
.box {
  border: green 1px dashed;
  margin: 10px;
}
</style>
