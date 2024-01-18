<script setup lang="ts">
import axios from "axios";
import { ref } from "vue";

const str = ref();

const copy = () => {
  navigator.clipboard.writeText(str.value);

};

const getKFC = () => {
  axios
    .get(
      "https://raw.githubusercontent.com/Nthily/KFC-Crazy-Thursday/main/kfc.json"
    )
    .then((res) => {
      const json = res.data;
      str.value = json[Math.floor(Math.random() * json.length)].text;
    });
};

getKFC();
</script>

<template>
  <div>
    <div class="title">
      <h1>KFC Crazy Thursday 文案</h1>
    </div>
    <div class="kfc-text">
      <span>{{ str }}</span>
    </div>
    <div class="btn">
      <div class="copy" @click="copy">复制</div>
      <div class="reload" @click="getKFC()">刷新</div>
    </div>
  </div>
</template>

<style scoped>
.kfc-text {
  padding: 20px;
  margin: 20px;
  min-height: 20vh;
  display: flex;
}
.copy {
  background-color: lightgreen;
}
.reload {
  background-color: lightblue;
}
.btn div {
  color: black;
  padding: 10px;
  margin: 0 10px 0 10px;
  width: 80px;
  border-radius: 25px;
  cursor: pointer;
}
.btn {
  display: flex;
  flex-direction: row;
  justify-content: end;
}
</style>
