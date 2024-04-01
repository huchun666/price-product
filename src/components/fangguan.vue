<template>
  <tr>
    <th rowspan="3">
      <button @click="decrease">-</button>
      <div class="label-title">方管</div>
      <button @click="add">+</button>
    </th>
    <td>周长</td>
    <td class="bg-input">
      <input type="number" v-model="zhouchang" />
    </td>
    <td>mm</td>
    <td>长度</td>
    <td class="bg-input"><input type="number" v-model="changdu" /></td>
    <td>m</td>
    <td>厚度</td>
    <td class="bg-input"><input type="number" v-model="houdu" /></td>
    <td>mm</td>
  </tr>
  <tr>
    <td>钢管单价</td>
    <td class="bg-input"><input type="number" v-model="gangguandj" /></td>
    <td>元/吨</td>
    <td>重量</td>
    <td class="zhongliang">
      {{ ((zhouchang - houdu) * houdu * 0.02466 * changdu).toFixed(2) }}
    </td>
    <td>KG</td>
    <td>喷塑面积</td>
    <td class="mianji">
      {{ ((3.14 * zhouchang * changdu) / 1000).toFixed(2) }}
    </td>
    <td>㎡</td>
  </tr>
  <tr>
    <td>钢管成本</td>
    <td class="chengben">
      {{
        (
          ((zhouchang - houdu) * houdu * 0.02466 * changdu * gangguandj) /
          1000
        ).toFixed(2)
      }}
    </td>
    <td>元</td>
  </tr>
</template>

<script setup>
import { ref } from "vue";
const emits = defineEmits(["decrease", "add"]);

const zhouchang = ref("");
const changdu = ref("");
const houdu = ref("");
const gangguandj = ref("");

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
