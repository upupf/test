<template>
    <div class="goodsitem" @click="itemClick">
        <img :src="goodsItem.show.img" alt="" @load="imageLoad">
        <div class="goodsinfo">
            <p>{{goodsItem.title}}</p>
            <span class="price">￥{{goodsItem.price}}</span>
            <span class="collect">{{goodsItem.cfav}}</span>
        </div>
    </div>
</template>

<script>
export default {
    name : 'GoodsListItem',
    props : {
        goodsItem : {
            type : Object,
            default () {
                return {}
            }
        }
    },
    methods : {
        imageLoad () {
            // console.log("imageLoad");
            this.$bus.$emit('itemImageLoad')
        },

        itemClick() {
            // 跳转到详情页
            // console.log('跳转详情页');
            this.$router.push('/detail/' + this.goodsItem.iid)
        }
    }
}
</script>

<style>
    .goodsitem {
        width: 45%;
        padding-bottom: 40px;
        position: relative;
    }

    .goodsitem img {
        width: 100%;
        border-radius: 5px;
    }

    .goodsinfo {
        font-size: 12px;
        position: absolute;
        bottom: 5px;
        left: 0;
        right: 0;
        overflow: hidden;
        text-align: center;
    }

    .goodsinfo p {
        overflow: hidden;
        text-overflow: ellipsis;
        white-space: nowrap;
        margin-bottom: 3px;
    }

    .goodsinfo .price {
        color: var(--color-high-text);
        margin-right: 20px;
    }

    .goodsinfo .collect {
        position: relative;
    }
</style>