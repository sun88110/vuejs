<template>
  <div>
    <button v-on:click="onClickFnc">클릭</button>
    <p>결과: {{ randValue }}</p>
  </div>
  <p><input type="text" v-model="msg" value="hhhh" /></p>
  <p v-bind:class="computedStyles">{{ msg }}</p>
</template>

<script setup>
import { ref, computed } from 'vue'

const randValue = ref('시작 전')
const msg = ref('Hello, World') //이거랑 v-model이랑 이어져있음 그래서 값바꾸면 같이 바뀜
let isRedFlag = ref(true)
let isBlueFlag = ref(true)
const computedStyles = computed(() => {
  return { txtColorRed: isRedFlag.value, bgColorBlue: isBlueFlag.value } // let으로 만들어서 value로 줘야됨
})

const onClickFnc = () => {
  const rand = Math.round(Math.random() * 100)
  randValue.value = rand

  isRedFlag.value = rand > 50 ? true : false
  isBlueFlag.value = rand > 50 ? true : false
}
</script>

<style scoped>
/* 페이지 전체 정렬 */
div {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 40px;
  font-family: 'Pretendard', 'Noto Sans KR', sans-serif;
}

/* 버튼 스타일 */
button {
  background-color: #2563eb; /* 파란색 */
  color: white;
  border: none;
  border-radius: 8px;
  padding: 10px 20px;
  font-size: 1rem;
  cursor: pointer;
  transition:
    background-color 0.25s,
    transform 0.1s;
}

button:hover {
  background-color: #1e40af;
}

button:active {
  transform: scale(0.96);
}

/* 결과 텍스트 */
p {
  font-size: 1.2rem;
  margin-top: 10px;
}

/* 동적으로 적용될 클래스들 */
.txtColorRed {
  color: #ef4444; /* 빨강 */
  font-weight: bold;
}

.bgColorBlue {
  background-color: #3b82f6; /* 파랑 배경 */
  color: white;
  padding: 12px 20px;
  border-radius: 10px;
  transition:
    background-color 0.3s,
    color 0.3s;
}

/* 애니메이션 효과 추가 (변화 시 자연스럽게) */
.txtColorRed,
.bgColorBlue {
  transition: all 0.3s ease;
}
</style>
