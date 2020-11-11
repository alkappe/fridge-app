<template>
  <div class="addItem">
    <form @submit="addItem">
      <input class="addItem__input" type="text" v-model="product" name="product" placeholder="type product 🥑 🦐 🐟">
      <button class="addItem__button" type="submit">Add</button>
    </form>
  </div>
</template>
<script>
import {v4} from 'uuid';
const uuId = v4()

export default {
  name: 'AddItem',
  data() {
    return {
      product: ''
    }
  },
  methods: {
    addItem(e) {
      e.preventDefault();
      const newTodoObj = {
        id: uuId,
        product: this.product,
        category: 'altro',
        completed: false
      }
      this.$emit('add-item', newTodoObj);
      this.product = '';
    }
  }
}
</script>
<style scoped>
  .addItem {
    position: relative;
    margin: 30px 0 10px 0;
  }

  @media screen and (min-width: 992px) {
    .addItem { 
      position: absolute;
      top: 0;
      right: 60px;
      margin: 0;
    }
  }

  .addItem__input {
    width: 150px;
    border: solid 3px #ECA72C;
    font-family: 'Permanent Marker', cursive;
  }

  .addItem__button {
    cursor: pointer;
    background: #fff;
    border-color: transparent;
    background: #ECA72C;
    border: solid 3px #ECA72C;
    margin-left: 4px;
  }
</style>