<template>
  <div>
    <p>이름: <input type="text" v-model="finfo.name" /></p>
    <p>나이: <input type="number" v-model="finfo.age" /></p>
    <p><button @click="addFriend">친구 추가</button></p>

    <table border="1">
      <thead>
        <tr>
          <th>이름</th>
          <th>나이</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="friend in friends" :key="friend.name">
          <td>{{ friend.name }}</td>
          <td>{{ friend.age }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup>
import { reactive } from "vue";

//Data.  reactive()를 안 쓰면 데이터는 바뀌지만,
//Vue가 그걸 모르기 때문에 화면이 업데이트되지 않는다.
const friends = reactive([
  { name: "홍길동", age: 20 },
  { name: "김민식", age: 21 },
]);

const finfo = reactive({
  name: "",
  age: 20,
});

// 친구 추가 함수
const addFriend = () => {
  friends.push({ name: finfo.name, age: finfo.age });
};
</script>
