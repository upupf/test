<template>
    <div class="goods">
        <GoodsListItem v-for="(item, index) in goods" :key="index" :goods-item="item"/>
          <!-- {{goods}}   -->
    </div>
</template>

<script>
import GoodsListItem from './GoodsListItem.vue'

export default {
    name : 'GoodsList',
    components : {
        GoodsListItem
    },
    props : {
        goods : {
            type : Array,
            default () {
                return []
            }
        }
    }
}
</script>

<style>
    .goods {
        display: flex;
        flex-wrap: wrap;
        justify-content: space-around;
    }
</style>