<template>
    <div class="fridge-level"> 
        <h2 class="fridge-level__title"> {{ categoriesTitle }}</h2>
        <!--<div v-for="item in matchItems(salumi)" v-bind:key="item.id">{{ item.product}}</div>-->
        <div class="fridge-level__line"></div>
    </div>
</template>
<script>

export default {

  components: {

  },
props: ['categoriesTitle']
}
</script>
<style scoped>
  
  
</style>