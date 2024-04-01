<template>
  <tr>
    <th rowspan="4">
      <button @click="decrease">-</button>
      <div class="label-title">圆锥主杆</div>
      <button @click="add">+</button>
    </th>
    <td>上口径</td>
    <td class="bg-input">
      <input type="number" v-model="shangkj" />
    </td>
    <td>mm</td>
    <td>下口径</td>
    <td class="bg-input"><input type="number" v-model="xiakj" /></td>
    <td>mm</td>
    <td>长度</td>
    <td class="bg-input"><input type="number" v-model="length" /></td>
    <td>m</td>
  </tr>
  <tr>
    <td>厚度</td>
    <td class="bg-input"><input type="number" v-model="houdu" /></td>
    <td>mm</td>
    <td>卷杆单价</td>
    <td class="bg-input"><input type="number" v-model="juangandj" /></td>
    <td>元/米</td>
    <td>钢板宽度</td>
    <td class="bg-input"><input type="number" v-model="gangbankd" /></td>
    <td>mm</td>
  </tr>
  <tr>
    <td>理算宽度</td>
    <td>{{ ((shangkj + xiakj - houdu - houdu) * 3.14).toFixed(2) }}</td>
    <td>mm</td>
    <td>卷杆成本</td>
    <td class="chengben">{{ juangandj * length }}</td>
    <td>元</td>
    <td>钢板单价</td>
    <td class="bg-input"><input type="number" v-model="gangbandj" /></td>
    <td>元/吨</td>
  </tr>
  <tr>
    <td>喷塑面积</td>
    <td class="mianji">
      {{
        (((shangkj + xiakj - houdu - houdu) * 3.14 * length) / 2000).toFixed(2)
      }}
    </td>
    <td>㎡</td>
    <td>镀锌重量</td>
    <td class="zhongliang">
      {{
        (
          ((shangkj + xiakj - houdu - houdu) * 3.14 * length * houdu * 7.85) /
          2000
        ).toFixed(2)
      }}
    </td>
    <td>KG</td>
    <td>钢板成本</td>
    <td class="chengben">
      {{
        ((gangbandj * gangbankd * length * houdu * 7.85) / 2000000).toFixed(2)
      }}
    </td>
    <td>元</td>
  </tr>
</template>

<script setup>
import { ref } from "vue";
const emits = defineEmits(["decrease", "add"]);

const shangkj = ref("");
const xiakj = ref("");
const length = ref("");
const houdu = ref("");
const juangandj = ref("");
const gangbankd = ref("");
const gangbandj = ref("");

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
