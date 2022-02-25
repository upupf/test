<template>
  <div class="recommend">
      <div class="recommend-item" v-for="(item,index) in recommends" :key="index">
          <a :href="item.link">
              <img :src="item.image" alt="">
              <div>{{item.title}}</div>
          </a>
      </div>
  </div>
</template>

<script>
export default {
    name : 'HomeRecommend',
    props : {
        recommends : {
            type : Array,
            default () {
                return []
            }
        }
    }
}
</script>

<style>
    .recommend {
        display: flex;
        padding: 10px 0;
        border-bottom: 20px solid #eee;
    }

    .recommend-item {
        flex: 1;
        text-align: center;
    }

    .recommend-item img {
        width: 80%;
        vertical-align: middle;
        margin-bottom: 10px;
    }
</style>