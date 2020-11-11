<template>
  <div>
    <h2 class="title">grocery shopping</h2>
    <div class="item-wrapper">
      <ul class="item-container">
        <li v-bind:key="item.id" v-for="item in items">
          <Item v-bind:item="item" v-on:store-item="$emit('store-item', item.id)"/>
        </li>
      </ul>
    </div>
  </div>
</template>
<script>
import Item from './Item';
export default {
  name: 'Items',
  components: {
    Item
  },
  props: [
    "items"
  ]
}
</script>
<style scoped>
  .title {
    font-size: 24px;
    text-transform: uppercase;
    padding-top: 40px;
  }

  .item-wrapper {
    overflow: hidden; 
    margin: 0 0;
  }

  @media screen and (min-width: 992px) {
    .item-wrapper { 
      overflow: auto;  
    }
  }

  .item-container {
    display: flex;
    list-style: none;
    text-decoration: none;
    margin: 0 0;
    padding-left: 0;
    overflow-x: scroll;
    overflow-y: hidden;
    justify-content: space-between;
  }

  @media screen and (min-width: 992px) {
    .item-container { 
      overflow: hidden; 
      flex-wrap: wrap;
      justify-content: stretch;
    }
  }
</style>