<template>
  <div v-bind:class="{'completed': item.completed}" v-on:click="sendInFridge" class="item">
    <p class="item__text" v-on:click="markComplete">{{ item.product }}</p>
    <button class="item__button" @click="$emit('store-item', item.id)">Store item</button>
  </div>
</template>
<script>
export default {
  name: 'item',
  props: [
    "item"
  ],
  methods: {
    markComplete() {
      this.item.completed = !this.item.completed
    },
    sendInFridge() {
      return this.item.category
    }
  }
}
</script>
<style scoped>

  .item {
    width: auto;
    min-width: 100px;
    margin: 5px 10px 5px 0;
  }

  @media screen and (min-width: 992px) {
    .item {
      margin: 5px 10px 5px 0;
    }
  }

  .item__text {
    text-align: center;
    padding: 10px 6px;
    margin: 0 0;
    background: #f2e94e;
  }

  .item__button {
    width: 100%;
    height: 28px;
    cursor: pointer;
    background: #fff;
    border-color: transparent;
    font-size: 14px;
  }

  .item__button:hover {
    background: #e73c7e;
    color: #fff;
  }

  /* thanks to https://manuelpinto.in */

 .item__button:hover {
    background: linear-gradient(-45deg, #ee7752, #e73c7e, #23a6d5, #23d5ab);
    background-size: 400% 400%;
    animation: gradient 5s ease infinite;
  }

  @keyframes gradient {
    0% {
      background-position: 0% 50%;
    }
    50% {
      background-position: 100% 50%;
    }
    100% {
      background-position: 0% 50%;
    }
  }


  
</style>