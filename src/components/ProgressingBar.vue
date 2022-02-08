<template>
  <div class="container">
    <div class="progress">
      <div class="progress-bar">
        <div class="progress-bar-background"></div>
        <div class="progress-bar-width" ref="progress"></div>
        <div v-for="n in progressTotalNum"
        :class="['progress-bar-item', {'progress-bar-item-active': recentPage >= n}]" :key="n">
          {{ n }}
        </div>
      </div>

      <div class="progress-btn-group">
        <button  @click="goPrev"
        :class="['progress-btn', {'progress-btn-disabled': recentPage === 1}]">
          Prev
        </button>
        <button  @click="goNext"
        :class="['progress-btn', {'progress-btn-disabled': recentPage === progressTotalNum}]">
          Next
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const progress = ref(null);
const progressTotalNum = ref(4);
const recentPage = ref(1);
const progerssWidth = ref(0);
const goPrev = () => {
  if (recentPage.value !== 1 && recentPage.value > 0) {
    recentPage.value -= 1;
    progress.value.style.width = `${(progerssWidth.value -= 1 / (progressTotalNum.value - 1)) * 100}%`;
  }
};
const goNext = () => {
  if (recentPage.value < progressTotalNum.value && recentPage.value !== progressTotalNum.value) {
    recentPage.value += 1;
    progress.value.style.width = `${(progerssWidth.value = (recentPage.value - 1) / (progressTotalNum.value - 1)) * 100}%`;
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
@import "@/assets/scss/index.scss";
.container {
  max-width: 30%;
  margin: 0 auto;
  padding: 3rem 0;
}
.progress {
  max-width: 100%;
}
.progress-bar{
  display: flex;
  justify-content: space-between;
  margin-bottom: 2rem;
  position: relative;
}
.progress-bar-background{
  width: 100%;
  height: 0.3rem;
  background: $info;
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  z-index: 1;
}
.progress-bar-width{
  width: 0%;
  height: 0.3rem;
  background: $secondary;
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  z-index: 2;
}
.progress-bar-item{
  position: relative;
  z-index: 3;
  width: 1.5rem;
  height: 1.5rem;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 50%;
  background-color: $white;
  color: $primary;
  border: 3px solid $primary;
}
.progress-bar-item-active{
  background-color: $primary;
  color: $white;
}
.progress-btn-group {
  display: flex;
  justify-content: center;
}
.progress-btn {
  margin: 0 0.5rem;
  background: $primary;
  color: $light;
  border-radius: 5px;
  border: 1px solid $primary;
  font-size: 1rem;
  padding: 0.5rem 1rem;
  cursor: pointer;
  &:hover {
    background: $secondary;
  }
  &:active{
    background: $dark;
  }
}
.progress-btn-disabled {
  cursor: not-allowed;
    background: $info;
    border: 1px solid $info;
  &:hover {
    cursor: not-allowed;
    background: $info;
    border: 1px solid $info;
  }
}
</style>
