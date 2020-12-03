<template>
    <div class="fridge-level"> 
        <h2 class="fridge-level__title">{{ categoriesTitle }}</h2>
        <div v-for="item in items" v-bind:key="item.id">{{ item.product }}</div>
        <div class="fridge-level__line"></div>
    </div>
</template>
<script>

export default {

    components: {

    },

    props: ['categoriesTitle', 'items']
}
</script>
<style scoped>
    .fridge-level {
        position: relative;
        margin-right: 10px;
        min-height: 200px;
        height: auto;
        background: aquamarine;
        padding: 0 10px;
    }

    @media screen and (min-width: 992px) {
        .fridge-level { 
        width: calc(50% - 20px);
        padding: 0;
        background: transparent;
        }

        .fridge-level:nth-child(odd) {
            margin-right: 10px;
        }

        .fridge-level:nth-child(even) {
            margin-left: 10px;
            margin-right: 0;
        }
    }

    .fridge-level__line {
        display: none;
    }

    @media screen and (min-width: 992px) {
        .fridge-level__line {
            display: block;
            position: absolute;
            bottom: 0;
            background: #000;
            height: 2px;
            animation-name: lineWidith;
            animation-duration: 3s;
            transition-timing-function: cubic-bezier(0.1, 0.7, 1.0, 0.1);
            animation-fill-mode: forwards;
        }
    }

    @keyframes lineWidith {
        from {width: 0%;}
        to {width: 100%;}
    }
</style>