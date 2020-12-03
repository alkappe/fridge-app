<template>
  <div id="app">
    <div class="search">
      <form class="search__form">
        <input class="search__input" type="text" v-model="searchItem"  placeholder="Search product 🔍︎ 😋">
      </form>
    </div>
    <AddItem v-on:add-item="addItem"/>
    <Items v-bind:items="matchItems(items)" v-on:store-item="storeItem"/>
    <div class="full-fridge-alert" v-show="items.length === 0">
      <mark>Products are all stored in the refrigerator</mark>
    </div>
    <div class="frige-wrapper">
      <div class="frige-container">
        <FridgeLevel v-for="category in categories" v-bind:key="category" v-bind:categories-title="category"
        v-bind:items="categoryItems(category)"></FridgeLevel>
      </div>
    </div>
  </div>
</template>
<script>

import Items from './components/Items';
import AddItem from './components/AddItem';
import FridgeLevel from './components/FridgeLevel';

export default {
  name: 'app',
  components: {
    Items,
    AddItem,
    FridgeLevel
  },
  props: {

  },
  data() {
    return {
      searchItem: '',
      categories: [
        'salumi',
        'formaggi',
        'verdure',
        'bibite',
        'altro'

      ],
      items: [
        {
          id: 1,
          product: 'Mortadella',
          expiration: 7,
          category: 'salumi',
          completed: false
        },
        {
          id: 2,
          product: 'Prosciutto crudo',
          expiration: 30,
          category: 'salumi',
          completed: false
        },
        {
          id: 3,
          product: 'Birra',
          expiration: 60,
          category: 'bibite',
          completed: false
        },
        {
          id: 4,
          product: 'Gorgonzola',
          category: 'formaggi',
          expiration: 4,
          completed: false
        },
        {
          id: 5,
          product: 'Pecorino',
          category: 'formaggi',
          expiration: 3,
          completed: false
        },
        {
          id: 6,
          product: 'Insalata fresca',
          category: 'verdure',
          expiration: 7,
          completed: false
        },
        {
          id: 7,
          product: 'Sedano',
          category: 'verdure',
          expiration: 5,
          completed: false
        },
        {
          id: 8,
          product: 'Peperoni',
          category: 'verdure',
          expiration: 8,
          completed: false
        },
        {
          id: 9,
          product: 'Coca cola',
          category: 'bibite',
          expiration: 365,
          completed: false
        },
        {
          id: 10,
          product: 'Vitello tonnato',
          category: 'altro',
          expiration: 15,
          completed: false
        },
      ],
      salumi: [],
      formaggi: [],
      verdure: [],
      bibite: [],
      altro: []
    }
  },
  methods: {
    addItem(newTodoObj) {
      this.items = [...this.items, newTodoObj];
    },
    storeItem(itemId) {
      const found = this.items.find(item => item.id === itemId);
      this.items = this.items.filter( item => item.id !== itemId);
      const arr = this[found.category]
      arr.push(found)
      arr.sort((item1, item2)  => item1.expiration - item2.expiration)
    },
    categoryItems(categoryName) {
      return this.matchItems(this[categoryName]);
    },
    matchItems(items) {
      if(this.searchItem === '') {
        return items
      }

      return items.filter( item => {
        return item.product.toLowerCase().startsWith(this.searchItem.toLowerCase());
      });
    },
    deleteItem(itemId) {
      this.items = this.items.filter( item => item.id !== itemId);
    }
  }
}
</script>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Permanent+Marker&display=swap');
</style>

<style>
  #app {
    font-family: 'Permanent Marker', cursive;
    margin: 60px 0;
    padding: 0 30px 0 40px;
    width: 100%;
    position: relative;
    box-sizing: border-box;
    background-color: #fff;
    /* thanks to http://projects.verou.me/css3patterns/ */
    background-image: linear-gradient(90deg, transparent 19px, #abced4 19px, #abced4 21px, transparent 1px), linear-gradient(#eee .1em, transparent .1em);
    background-size: 100% 1.2em;
  }

  @media screen and (min-width: 992px) {
    #app { 
      padding: 0 60px 0 120px;
      /* thanks to http://projects.verou.me/css3patterns/ */
      background-image:
      linear-gradient(90deg, transparent 79px, #abced4 79px, #abced4 81px, transparent 81px),
      linear-gradient(#eee .1em, transparent .1em);
      background-size: 100% 1.2em;
    }
  }

  .search__form {
    height: 100%;
  }

  .search {
    position: relative;
    height: 18px;
  }

  .search__input {
    width: 150px;
    border: solid 3px #A3D9FF;
    font-family: 'Permanent Marker', cursive;
  }

  .search__btn {
    cursor: pointer;
    background: #fff;
    border-color: transparent;
    background: #A3D9FF;
    border: solid 3px #A3D9FF;
    margin-left: 4px;
  }


  .fridge-wrapper {
    overflow: hidden;
  } 

  @media screen and (min-width: 992px) {
    .fridge-wrapper { 
    }
  }

  .frige-container { 
    overflow-x: scroll;
    display: flex;
    margin-top: 30px;
  }

  @media screen and (min-width: 992px) {
    .frige-container { 
      display: flex;
      flex-wrap: wrap;
      margin-top: 30px;
      justify-content: space-between;
    }
  }

  .full-fridge-alert {
    font-size: 28px;
    width: auto;
  }

  .full-fridge-alert > mark  {
    background: #7AE582;
  }

  button {
    font-family: 'Permanent Marker', cursive;
  }

  button:focus {
    outline:0; 
  }

  input {
    outline:0; 
  }
</style>