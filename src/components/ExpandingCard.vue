<template>
  <div class="container">
    <ul class="card-list">
      <li class="card-item" v-for="(item, index) in list" :key="item.id">
        <div class="card-title">
          <p>{{ item.title }}</p>
          <a @click="toggleDetails(index)" class="card-link" href="#">
            <i v-if="index !== recentShowContentindex" class="fas fa-plus card-icon-plus"></i>
            <i v-elseß class="fas fa-minus card-icon-plus"></i>
          </a>
        </div>
        <div v-if="recentShowContentindex === index" class="card-details">
          <p>
            {{ item.details }}
          </p>
        </div>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { reactive, ref } from 'vue';

const list = reactive([
  {
    id: 1,
    title: '請問我可以退貨嗎？',
    status: false,
    details: '商品若有非人為的瑕疵，即可在七天鑑賞期內退貨。',
  },
  {
    id: 2,
    title: '請問可以在哪裡聯絡到你？',
    details: 'Instagram: vivian_enlife',
    status: false,
  },
  {
    id: 3,
    title: '萬一商品在鑑賞期後因非人為因素而損壞，該怎麼辦？',
    details: '若有商品上的問題，歡迎私訊粉專！',
    status: false,
  },
]);
const recentShowContentindex = ref();
const toggleDetails = (index) => {
  // eslint-disable-next-line no-param-reassign
  list[index].status = !list[index].status;
  if (recentShowContentindex.value === index) {
    recentShowContentindex.value = null;
  } else {
    recentShowContentindex.value = index;
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.container {
  max-width: 50%;
  margin: 0 auto;
  padding: 50px 0;
}
.card-title {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.card-list {
  max-width: 100%;
  color: #343a40;
  border: 1px solid #3d405b;
  border-radius: 5px;
}

.card-item {
  border-bottom: 1px solid #3d405b;
  padding: 10px 20px;
  &:last-child {
    border-bottom: none;
  }
}
.card-link {
  display: inline-block;
}
.card-icon-plus {
  color: #343a40;
}
.card-details{
  padding: 20px;
  color: #023047;
}
.disabled {
  display: none;
}
</style>
