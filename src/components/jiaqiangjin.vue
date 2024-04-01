<template>
  <tr>
    <th rowspan="2">
      <button @click="decrease">-</button>
      <div class="label-title">加强筋</div>
      <button @click="add">+</button>
    </th>
    <td>重量</td>
    <td class="bg-input">
      <input type="number" v-model="zhongliang" class="zhongliang" />
    </td>
    <td>KG</td>
    <td>喷塑面积</td>
    <td class="bg-input">
      <input type="number" v-model="supengmj" class="mianji" />
    </td>
    <td>㎡</td>
    <td>单价</td>
    <td class="bg-input"><input type="number" v-model="danjia" /></td>
    <td>元/吨</td>
  </tr>
  <tr>
    <td>加强筋成本</td>
    <td class="chengben">{{ ((zhongliang * supengmj) / 1000).toFixed(2) }}</td>
    <td>元</td>
  </tr>
</template>

<script setup>
import { ref } from "vue";
const emits = defineEmits(["decrease", "add"]);

const zhongliang = ref("");
const supengmj = ref("");
const danjia = ref("");

const decrease = () => {
  emits("decrease");
};
const add = () => {
  emits("add");
};
</script>

<style scoped lang="less">
table {
  border-collapse: collapse;
}
td,
th {
  border: 1px solid black;
  padding: 10px 20px;
  background: rgb(201, 228, 180);
}
.bg-input {
  background: #fff;
}
input {
  border: 0;
  outline: none;
  font-size: 16px;
  width: 80px;
  text-align: center;
}
button {
  outline: none;
  border: 0;
  background-color: #c9e4b4;
}
.label-title {
  margin: 10px 0;
}
</style>
