<script setup>
// Vue.js 특징 1. 데이터변경 -> 화면(DOM update) refresh.

import { reactive, ref, computed } from "vue";

const url = ref("https://vuejs.org/");
const isDisabled = ref(true);
const imgAttributes = reactive({
  src: "/src/assets/logo.svg",
  alt: "Vue 기본 로고",
  width: "150px",
});
const txtColor = ref("pink");
const backColor = ref("green");
const styleAttributes = reactive({
  color: "pink",
  backgroundColor: "green",
});
const msg = ref("Hell, World");
const isTxtColorRed = ref(true);
const isBgColorBlue = ref(true);
const classstyles = reactive({
  txtColorRed: true,
  bgColorBlue: false,
  txtSize24: true,
});

// data 속성.
let isRedTrue = ref(true); // .value
let isBlueTrue = ref(true);

// data 속성.
const computedStyles = computed(() => {
  isRedTrue = ref(Math.round(Math.random())); // 0, '', null => falsy math.round는 반올림 0.5 이상은 1 아니면 0   0이면 거짓 1이면 참
  isBlueTrue = ref(Math.round(Math.random())); //여기값이 ref(true에 들어감)
  //   isRedTrue = isRedTrue == 0 ? false : true;
  //   isBlueTrue = isBlueTrue == 0 ? false : true;

  return { txtColorRed: isRedTrue.value, bgColorBlue: isBlueTrue.value };
});

setInterval(() => {
  const isRed = Math.round(Math.random()) == 0 ? false : true;
  const isBlue = Math.round(Math.random()) == 0 ? false : true;
  //   isRedTrue.value = Math.round(Math.random()); <- 이거 두개 주석해제하면 잘돌아감 대신 위에꺼 주석처리해야됨
  //   isBlueTrue.value = Math.round(Math.random()); // 지금은 콘솔만 찍히게 해놧음
  console.log(isRed, isBlue);

  //console.log(isRedTrue._value, isBlueTrue._value);
}, 100);
</script>

<template>
  <p>
    <a v-bind:href="url" v-bind:style="{ color: txtColor, backgroundColor: backColor }">
      Vue.js 사이트
    </a>
  </p>
  <p>
    <a v-bind:href="url + 'guide/introduction.html'" v-bind:style="styleAttributes">
      Vue.js 가이드페이지
    </a>
  </p>
  <p>
    <button v-bind:disabled="isDisabled">클릭</button>
  </p>
  <p>
    <img alt="Vue 로고" v-bind="imgAttributes" />
  </p>

  <p v-bind:class="{ txtColorRed: isTxtColorRed, isBgColorBlue }">{{ msg }}</p>
  <p v-bind:class="{ 'txt-color-pink': isTxtColorRed, isBgColorBlue }">{{ msg }}</p>
  <p v-bind:class="classstyles">{{ msg }}</p>
  <p v-bind:class="computedStyles">{{ msg }}</p>
</template>

<style scopd>
.txtColorRed {
  color: red;
}
.txt-color-pink {
  color: pink;
}
.bgColorBlue {
  background-color: blue;
}

.txtSize24 {
  font-size: 24px;
}
</style>
