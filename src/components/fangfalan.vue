<template>
  <tr>
    <th rowspan="3">
      <button @click="decrease">-</button>
      <div class="label-title">方法兰</div>
      <button @click="add">+</button>
    </th>
    <td>长</td>
    <td class="bg-input">
      <input type="number" v-model="chang" />
    </td>
    <td>mm</td>
    <td>宽</td>
    <td class="bg-input"><input type="number" v-model="kuan" /></td>
    <td>mm</td>
    <td>厚度</td>
    <td class="bg-input"><input type="number" v-model="houdu" /></td>
    <td>mm</td>
  </tr>
  <tr>
    <td>法兰单价</td>
    <td class="bg-input"><input type="number" v-model="falandj" /></td>
    <td>元/吨</td>
    <td>数量</td>
    <td class="bg-input">
      <input type="number" v-model="shuliang" />
    </td>
    <td>块</td>
    <td>喷塑面积</td>
    <td class="mianji">
      {{ ((chang * kuan * shuliang * 2) / 1000000).toFixed(2) }}
    </td>
    <td>㎡</td>
  </tr>
  <tr>
    <td>重量</td>
    <td class="zhongliang">
      {{ ((chang * kuan * houdu * 7.85 * shuliang) / 1000000).toFixed(2) }}
    </td>
    <td>KG</td>
    <td>法兰成本</td>
    <td class="chengben">
      {{
        (
          (((chang * kuan * houdu * 7.85 * shuliang) / 1000000) * falandj) /
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

const chang = ref("");
const kuan = ref("");
const houdu = ref("");
const shuliang = ref("");
const falandj = ref("");

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
