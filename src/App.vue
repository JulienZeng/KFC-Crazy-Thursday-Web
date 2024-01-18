<script setup lang="ts">
import axios from "axios";
import { ref } from "vue";

const str = ref("正在获取文案，请稍候...");
// const json = ref();
// const reget = ref(true);

const copy = () => {
  navigator.clipboard.writeText(str.value);
};

const ICPInfo = {
  icpNo: "粤ICP备2022014957号-1",
  psbNo: "粤公网安备 44049102496850号",
  psbLogoURL: "https://beian.mps.gov.cn/img/logo01.dd7ff50e.png",
  icpRecoadURL: "https://beian.miit.gov.cn/",
  psbRecoadURL:
    "http://www.beian.gov.cn/portal/registerSystemInfo?recordcode=44049102496850",
};

// const reflash = () => {
//   if (json) {
//     reget.value = false;
//   } else {
//     reget.value = true;
//   }
//   getKFC();
// };

const getKFC = () => {
  // if (reget) {
  //   axios
  //     .get(
  //       "https://raw.githubusercontent.com/Nthily/KFC-Crazy-Thursday/main/kfc.json"
  //     )
  //     .then((res) => {
  //       json.value = res.data;
  //       str.value =
  //         json.value[Math.floor(Math.random() * json.value.length)].text;
  //     })
  //     .catch((err) => {
  //       str.value = "网络连接失败，请刷新重试。";
  //       console.log(err);
  //     });
  // } else {
  //   str.value = json.value[Math.floor(Math.random() * json.value.length)].text;
  // }
  axios
    .get("https://api.jixs.cc/api/wenan-fkxqs/index.php")
    .then((res) => {
      str.value = res.data;
    })
    .catch((err) => {
      str.value = "网络连接失败，请刷新重试。";
      console.log(err);
    });
};

getKFC();
</script>

<template>
  <div style="flex: 1">
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
  <div class="footer">
    <div class="icp">
      <a :href="ICPInfo.icpRecoadURL">{{ ICPInfo.icpNo }}</a>
    </div>
    <div class="psb">
      <img class="psb-logo" :src="ICPInfo.psbLogoURL" />
      <a :href="ICPInfo.psbRecoadURL">{{ ICPInfo.psbNo }}</a>
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
.footer {
  display: flex;
  flex-direction: column;
  margin: 20px 0 20px 0;
}
.icp {
  margin: 10px 0 10px 0;
  display: flex;
  justify-content: center;
  align-items: center;
}
.psb {
  margin: 10px 0 10px 0;
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
}
.psb-logo {
  width: 20px;
  height: 20px;
}
</style>
