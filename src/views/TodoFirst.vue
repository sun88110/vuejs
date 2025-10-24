<script setup>
import { ref } from "vue";
const url = ref("https://vuejs.org/");
const footMsg = ref("& 2025 나의 웹페이지 모든 권리 보유");
</script>

<template>
  <header>
    <h1>나의 첫 웹 페이지</h1>
    <p>HTML과 CSS로 만든 기본 구조</p>
  </header>
  <body>
    <h2>환영합니다!</h2>
    <p>이 페이지는 HTML과 CSS로 만들어졌으며, 기본적인 구조와 스타일을 포함하고 있습니다.</p>
    <ul>
      <dt>내용 예시</dt>
      <li>간단한 텍스트</li>
      <li>링크 <a v-bind:href="url + 'guide/introduction.html'">예시 사이트</a></li>
      <li>리스트 항목</li>
    </ul>
  </body>
  <footer>{{ footMsg }}</footer>
</template>

<style scoped>
/* 전체 기본 레이아웃 */

html {
  background-color: #e5e7eb; /* 밝은 회색 (#e5e7eb는 Tailwind gray-200 정도) */
}

body {
  font-family: "Pretendard", "Noto Sans KR", sans-serif;
  background-color: #f8fafc;
  color: #333;
  line-height: 1.6;
  margin: 10px auto;
  max-width: 700px;
  padding: 1px;
}

/* 헤더 */
header {
  text-align: center;
  background-color: #40bd48;
  color: white;
  padding: 20px 0;
  border-radius: 10px;
}

header h1 {
  margin: 0;
  font-size: 1.8rem;
}

header p {
  margin: 5px 0 0;
  font-size: 1rem;
  opacity: 0.9;
}

/* 본문 텍스트 */
p {
  margin-bottom: 20px;
}

/* 정의 리스트 */
dl {
  background: white;
  padding: 15px 20px;
  border-radius: 8px;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
}

dt {
  font-weight: bold;
  margin-bottom: 8px;
  color: #2563eb;
}

dd {
  margin-left: 10px;
  margin-bottom: 8px;
}

/* 링크 스타일 */
a {
  color: #2563eb;
  text-decoration: none;
  font-weight: 500;
}

a:hover {
  text-decoration: underline;
}
</style>
