<template>
  <div class="container">
    <div class="title">科华集团</div>
    <table>
      <yuanzhui
        v-for="(item, index) in yuanzhuiList"
        :key="item"
        @add="addyuanzhui"
        @decrease="decreaseyuanzhui(index)"
      ></yuanzhui>
      <yuanguan
        v-for="(item, index) in yuanguanList"
        :key="item"
        @add="addyuanguan"
        @decrease="decreaseyuanguan(index)"
      ></yuanguan>
      <fangguan
        v-for="(item, index) in fangguanList"
        :key="item"
        @add="addfangguan"
        @decrease="decreasefangguan(index)"
      ></fangguan>
      <fangfalan
        v-for="(item, index) in fangfalanList"
        :key="item"
        @add="addfangfalan"
        @decrease="decreasefangfalan(index)"
      ></fangfalan>
      <jiaqiangjin
        v-for="(item, index) in jiaqiangjinList"
        :key="item"
        @add="addjiaqiangjin"
        @decrease="decreasejiaqiangjin(index)"
      />
      <tr>
        <th>镀锌费用</th>
        <td>镀锌单价</td>
        <td class="bg-input"><input type="number" v-model="duxindj" /></td>
        <td>元/吨</td>
        <td>总重量</td>
        <td>{{ zongzhongliang.toFixed(2) }}</td>
        <td>KG</td>
        <td>镀锌总价</td>
        <td>{{ ((zongzhongliang * duxindj) / 1000).toFixed(2) }}</td>
        <td>元</td>
      </tr>
      <tr>
        <th>喷塑费用</th>
        <td>喷塑单价</td>
        <td class="bg-input"><input type="number" v-model="pensudj" /></td>
        <td>元/㎡</td>
        <td>总面积</td>
        <td>{{ zongmianji.toFixed(2) }}</td>
        <td>㎡</td>
        <td>喷塑总价</td>
        <td>{{ (zongmianji * pensudj).toFixed(2) }}</td>
        <td>元</td>
      </tr>
      <tr>
        <th>其他</th>
        <td>做工</td>
        <td class="bg-input"><input type="number" v-model="zuogong" /></td>
        <td>元/套</td>
        <td>耗材</td>
        <td class="bg-input"><input type="number" v-model="haochai" /></td>
        <td>元/套</td>
        <td>杂费</td>
        <td class="bg-input"><input type="number" v-model="zafei" /></td>
        <td>元/套</td>
      </tr>
      <tr>
        <td colspan="2">总成本</td>
        <td colspan="2">{{ totalcb.toFixed(2) }}</td>
        <td>元/套</td>
        <td colspan="2">重量成本</td>
        <td colspan="2">
          {{ ((totalcb * zongzhongliang) / 1000).toFixed(2) }}
        </td>
        <td>元/吨</td>
      </tr>
    </table>
    <button class="start-judge" @click="start">开始计算</button>
  </div>
</template>

<script setup>
import yuanzhui from "./components/yuanzhui.vue";
import yuanguan from "./components/yuanguan.vue";
import fangguan from "./components/fangguan.vue";
import fangfalan from "./components/fangfalan.vue";
import jiaqiangjin from "./components/jiaqiangjin.vue";
import { ref } from "vue";
const yuanzhuiList = ref([1]);
const yuanguanList = ref([1]);
const fangguanList = ref([1]);
const fangfalanList = ref([1]);
const jiaqiangjinList = ref([1]);
const duxindj = ref("");
const pensudj = ref("");
const zuogong = ref("");
const haochai = ref("");
const zafei = ref("");
const totalcb = ref(0);
const zongzhongliang = ref(0);
const zongmianji = ref(0);
const addyuanzhui = () => {
  yuanzhuiList.value.push(yuanzhuiList.value.length + 1);
};
const decreaseyuanzhui = (index) => {
  yuanzhuiList.value.splice(index, 1);
};
const addyuanguan = () => {
  yuanguanList.value.push(yuanguanList.value.length + 1);
};
const decreaseyuanguan = (index) => {
  yuanguanList.value.splice(index, 1);
};
const addfangguan = () => {
  fangguanList.value.push(fangguanList.value.length + 1);
};
const decreasefangguan = (index) => {
  fangguanList.value.splice(index, 1);
};
const addfangfalan = () => {
  fangfalanList.value.push(fangfalanList.value.length + 1);
};
const decreasefangfalan = (index) => {
  fangfalanList.value.splice(index, 1);
};
const addjiaqiangjin = () => {
  jiaqiangjinList.value.push(jiaqiangjinList.value.length + 1);
};
const decreasejiaqiangjin = (index) => {
  jiaqiangjinList.value.splice(index, 1);
};
const start = () => {
  zongzhongliang.value = 0;
  let zhongliang = [...document.querySelectorAll(".zhongliang")];
  zhongliang.forEach((el) => {
    if (el.innerHTML) {
      zongzhongliang.value = Number(el.innerHTML) + zongzhongliang.value;
    } else {
      zongzhongliang.value = Number(el.value) + zongzhongliang.value;
    }
  });

  zongmianji.value = 0;
  let mianji = [...document.querySelectorAll(".mianji")];
  mianji.forEach((el) => {
    if (el.innerHTML) {
      zongmianji.value = Number(el.innerHTML) + zongmianji.value;
    } else {
      zongmianji.value = Number(el.value) + zongmianji.value;
    }
  });

  totalcb.value = 0;
  let chengben = [...document.querySelectorAll(".chengben")];
  chengben.forEach((el) => {
    totalcb.value = Number(el.innerHTML) + totalcb.value;
  });
};
</script>

<style scoped lang="less">
.container {
  .title {
    font-size: 40px;
    margin-bottom: 20px;
    font-weight: bold;
  }
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
    text-align: center;
  }
  input {
    border: 0;
    outline: none;
    font-size: 16px;
    width: 80px;
  }
  button {
    outline: none;
    border: 0;
    background-color: #c9e4b4;
  }
  .label-title {
    margin: 10px 0;
  }
  .start-judge {
    margin-top: 40px;
    width: 200px;
    height: 50px;
    font-size: 16px;
    background: #ddd;
  }
}
</style>
