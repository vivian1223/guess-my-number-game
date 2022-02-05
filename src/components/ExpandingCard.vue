<template>
  <div class="container">
      <ul class="card-list">
        <li class="card-item" v-for="item in list" :key="item.id">
          <div class="card-title">
            <p>{{ item.title }}</p>
            <a class="card-link" href="#"><i class="fas fa-plus card-icon-plus"></i></a>
          </div>
        </li>
      </ul>
  </div>
</template>

<script setup>
const list = [
  {
    id: 1,
    title: '請問我可以退貨嗎？',
    content: '可以唷！',
  },
  {
    id: 2,
    title: '請問我可以退貨嗎？',
    content: '可以唷！',
  },
];
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

.container{
  max-width: 50%;
  margin: 0 auto;
  padding: 50px 0;
}
.card-title{
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.card-list{
  max-width: 100%;
  color: #343a40;
  border: 1px solid #3d405b;
  border-radius: 5px;
}

.card-item {
  border-top: 1px solid #3d405b;
  padding: 10px 20px;
  margin-top: -1px;
}
.card-link{
  display: inline-block;
}
.card-icon-plus{
color: #343a40;
}
</style>
