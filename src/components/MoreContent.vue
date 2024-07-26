<template>
  <div class="more-content">
    <div class="time-title" v-if="!common.isEmpty(state.time.countdownTime)">
      {{ state.countdownChange }}
    </div>
  </div>
</template>

<script setup>
import common from "@/utils/common";
import { reactive } from "vue";

const state = reactive({
  time: {
    countdownTime: "2099-9-26 17:30:00",
  },
  countdownChange: "",
});

const countdown = () => {
  if (common.isEmpty(state.time.countdownTime)) {
    return;
  }
  let now = new Date();
  if (xiuxi(now)) {
    state.countdownChange = "别卷了，好好休息吧~";
  } else {
    let countdown = common.countdown(state.time.countdownTime, now);
    state.countdownChange =
      "下班倒计时: " + countdown.h + "时" + countdown.m + "分" + countdown.s + "秒";
  }
};
const xiuxi = (now) => {
  let weekDay = now.getDay();
  let hour = now.getHours();
  let minute = now.getMinutes();
  if (weekDay == 0 || weekDay == 6) {
    return true;
  }
  if (hour > 17 || (hour == 17 && minute >= 30)) {
    return true;
  }
  if (hour < 8 || (hour == 8 && minute < 30)) {
    return true;
  }
  return false;
};

setInterval(() => {
  countdown();
}, 1000);
</script>

<style lang="scss" scoped>
.more-content {
  display: flex;
  align-items: center;
  justify-content: center;
  margin-top: 20px;
  width: 100%;
  height: 100%;
}
.time-title {
  text-align: center;
  font-size: 1.5rem;
  line-height: 4rem;
  font-weight: 600;
  letter-spacing: 2px;
}
</style>
