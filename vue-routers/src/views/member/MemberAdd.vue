<template>
  <h3>회원관리</h3>
  <nav id="breadcrums">
    <ul>
      <li><RouterLink v-bind:to="{ name: 'AppTop' }">TOP</RouterLink></li>
      <li><RouterLink v-bind:to="{ name: 'MemberList' }">회원리스트</RouterLink></li>
      <li>회원정보추가</li>
    </ul>
  </nav>
  <section>
    <h3>회원정보추가</h3>
    <p>회원정보를 입력하고 추가버튼을 클릭하세요.</p>
    <form v-on:submit.prevent="onAdd">
      <dl>
        <dt><label for="">ID</label></dt>
        <dd><input type="number" v-model="member.id" /></dd>
        <dt><label for="">이름</label></dt>
        <dd><input type="text" v-model="member.name" /></dd>
        <dt><label for="">이메일</label></dt>
        <dd><input type="email" v-model="member.email" /></dd>
        <dt><label for="">포인트</label></dt>
        <dd><input type="number" v-model="member.points" /></dd>
        <dt><label for="">비고</label></dt>
        <dd><input type="text" v-model="member.note" /></dd>
      </dl>
      <button type="submit">생성</button>
    </form>
  </section>
</template>

<script setup>
import { inject, reactive } from 'vue'
import { useRouter } from 'vue-router'
// import axios from 'axios' https://axios-http.com/kr/docs/post_example <-여기로 들어가서 꼭해보셈

const router = useRouter()

// data.
const member = reactive({
  id: 0,
  name: '',
  email: '',
  points: 0,
  note: '',
})
const memberList = inject('memberList')
//함수
const onAdd = () => {
  memberList.set(member.id, member)
  // 목록이동
  router.push({ name: 'MemberList' })
}
</script>
