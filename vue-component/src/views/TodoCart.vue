<template>
  <h2>🛒 장바구니</h2>

  <div style="margin-bottom: 1rem">
    <label>상품코드: <input type="text" v-model="code" /></label><br />
    <label>상품명: <input type="text" v-model="name" /></label><br />
    <label>가격: <input type="number" v-model="price" min="0" /></label><br />
    <label>수량: <input type="number" v-model="qty" min="1" /></label><br />
    <button v-on:click="addItem">상품 추가</button>
  </div>

  <table border="1" cellspacing="0" cellpadding="5">
    <thead>
      <tr style="background-color: #eee">
        <th>상품코드</th>
        <th>상품명</th>
        <th>가격</th>
        <th>수량</th>
        <th>합계</th>
        <th>삭제</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="item in cartItems.values()" v-bind:key="item.id">
        <td>{{ item.itemCode }}</td>
        <td>{{ item.itemName }}</td>
        <td>{{ formatCurrency(item.price) }}</td>
        <td>
          <input type="number" min="1" style="width: 60px" v-model.number="item.qty" />
        </td>
        <td>{{ formatCurrency(getItemTotal(item.price, item.qty)) }}</td>
        <td>
          <button v-on:click="removeItem(item.id)">❌</button>
        </td>
      </tr>
    </tbody>
    <tfoot>
      <tr>
        <th colspan="4" style="text-align: right">총합계:</th>
        <th colspan="2">{{ formatCurrency(grandTotal) }}</th>
      </tr>
    </tfoot>
  </table>
</template>

<script setup>
import { ref, reactive, computed } from 'vue'

// 1. 입력 폼의 상태 (ref)
const code = ref('')
const name = ref('')
const price = ref(0)
const qty = ref(1)

// 2. 장바구니 데이터 (reactive Map 사용)
const cartItems = reactive(new Map())
let nextId = 1

// 초기 데이터 설정
cartItems.set(nextId, {
  id: nextId++,
  itemCode: 'P001',
  itemName: '무선마우스',
  price: 15000,
  qty: 1,
})

// 3. 상품 추가 함수 (중복 코드를 새 항목으로 추가하는 기본 로직)
const addItem = () => {
  // 필수 필드 및 유효성 검사 (0 이하 값 방지)
  if (!code.value || !name.value || price.value <= 0 || qty.value <= 0) {
    alert('모든 상품 정보를 올바르게 입력해주세요.')
    return
  }

  // 상품 정보 생성
  const newItem = {
    id: nextId++,
    itemCode: code.value,
    itemName: name.value,
    price: price.value,
    qty: qty.value,
  }

  cartItems.set(newItem.id, newItem)

  // 입력 필드 초기화
  code.value = ''
  name.value = ''
  price.value = 0
  qty.value = 1
}

// 4. 상품 삭제 함수
const removeItem = (id) => {
  cartItems.delete(id)
}

// 5. 상품별 합계 계산 함수
const getItemTotal = (price, qty) => {
  return price * qty
}

// 6. 총합계 계산 (Computed 속성)
const grandTotal = computed(() => {
  let total = 0
  for (const item of cartItems.values()) {
    // NaN 방지: 수량이 유효한 숫자가 아닐 경우 0으로 처리 (v-model.number가 대부분 처리함)
    const currentQty = isNaN(item.qty) || item.qty < 0 ? 0 : item.qty
    total += item.price * currentQty
  }
  return total
})

// 금액을 원화 포맷으로 변환하는 도우미 함수
const formatCurrency = (amount) => {
  // 금액이 유효한 숫자인지 확인
  if (typeof amount !== 'number' || isNaN(amount)) {
    return '0원'
  }
  return amount.toLocaleString('ko-KR') + '원'
}
</script>

<style scoped>
table {
  width: 100%;
  border-collapse: collapse;
}
input[type='text'],
input[type='number'] {
  margin: 3px 0;
}
button {
  margin-top: 5px;
}
</style>
