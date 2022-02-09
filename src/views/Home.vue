<template>
  <div class="container">
    <div class="header">
      <p class="hedaer-title">
       Between 1 and 20
      </p>
      <button @click="getNewGame">
        Again!
      </button>
    </div>
    <div class="content">
      <h1 class="h1">
        Guess My Number!
      </h1>
      <p class="content-score">score: {{ score }}</p>
      <div class="guess-box">
        {{ ramdomNum === answer ? answer :'?' }}
      </div>
      <p>{{ message }}</p>
    </div>
      <div class="play-box">
        <input v-model="guess" class="play-input" type="text">
        <button
        v-show="ramdomNum !== answer"
        :class="{'disabled': score < 0}" @click="check">
          Check!
        </button>
        <button v-show="ramdomNum === answer" @click="nextGuess">
          Keep Going!
        </button>
      </div>
  </div>
</template>

<script setup>
import { ref, watch } from 'vue';

// 隨機產生出 1 到 10 之間的號碼
const ramdomNum = ref(null);
const getRandomNum = () => {
  ramdomNum.value = Math.trunc(Math.random() * 20) + 1;
};
getRandomNum();
// 玩家猜的數字
const guess = ref(1);
// 正確答案
const answer = ref(null);
// 遊戲邏輯： 預設分數為 10
const score = ref(10);
// 提示訊息
const message = ref('Go!');
// 猜對後：
// 可以繼續往下猜並且分數+1
// play-box 要出現正確答案
// show message: Good Job!
// 猜錯的話：
// 如果分數還夠就 -2 且繼續往下猜直到猜對
// 根據 user 填入的數字去做比較
// 如果比 guess 小，就 log : Higher!
// 如果比 guess 大，就 log: lower!
// 分數不夠顯示 game over 並且把 check 按鈕 disabled 掉
const check = () => {
  if (Number(guess.value) === ramdomNum.value) {
    score.value += 3;
    message.value = "Good Job! Click 'Keep goning!' to move on";
    answer.value = Number(guess.value);
  } else if (Number(guess.value) >= ramdomNum.value && Number(guess.value) > 0) {
    score.value -= 2;
    message.value = 'Lower!';
  } else if (Number(guess.value) <= ramdomNum.value && Number(guess.value) > 0) {
    score.value -= 2;
    message.value = 'Higher!';
  } else {
    message.value = 'Only Numbers between 1 and 20 !';
  }
};
const nextGuess = () => {
  getRandomNum();
  message.value = 'Go!';
};
// reset:
// 當分數歸零時就只能將遊戲 reset
// 此時重置 user 的分數重置為十分
watch(score, (newVal) => {
  if (newVal < 0) {
    message.value = "Game over ! Click 'Again!' to start a new game!";
  }
});
const getNewGame = () => {
  score.value = 10;
  message.value = 'Go!';
  guess.value = 1;
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
@import "@/assets/scss/index.scss";

.container {
  background: linear-gradient(173deg, $primary 18%, $secondary 53%, $white 95%);
  width: 100%;
  min-height: 100vh;
  color: $dark;
    padding: 2rem;
}
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 4rem;
  @include tablet {
    flex-wrap: wrap;
    justify-content: center;
    margin-bottom: 3rem;
  }
}
.hedaer-title{
  color: $white;
  @include tablet {
    margin-bottom: 1rem;
  }
}
.content{
  display: flex;
  align-items: center;
  flex-direction: column;
  margin-bottom: 2rem;
}
.content-score{
  margin-bottom: 2rem;
}
.h1 {
  font-size: 3rem;
  margin-bottom: 3rem;
  @include tablet {
    font-size: 1.2rem;
  }
}
.guess-box {
  width: 10rem;
  height: 10rem;
  background: $light;
  color: $white;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 5rem;
  border: 4px solid $dark;
  margin-bottom: 2rem;
}
.play-box {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.play-input{
  border: 4px solid $dark;
  font-size: 3rem;
  padding: 1rem;
  margin-bottom: 2rem;
  font-family: inherit;
  width: 9rem;
}
.play-detail{
  margin-left: 3rem;
}
.play-message{
  margin-bottom: 2rem;
}

.disabled {
  cursor: not-allowed;
  color: #f0ebeb;
  border:4px solid #f0ebeb;;
}

button {
  font-family: inherit;
  color: inherit;
  padding: 1rem;
  border: 2px solid $dark;
  cursor: pointer;
  background: $white;
  &:active {
    background: #f0ebeb;
    color: #4b3d35;
  }
}
</style>
