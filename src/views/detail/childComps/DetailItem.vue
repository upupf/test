<template>
  <div>
    <NavBar>
      <div slot="left" class="left-back" @click="backClick">&lt;</div>
      <div slot="center"  class="title">
        <div v-for="(item, index) in titles" :key="index" 
              class="title-item" :class="{active : currentIndex === index}" @click="titleClick(index)">
          {{item}}
        </div>
      </div>
    </NavBar>
  </div>
</template>

<script>
import NavBar from '@/components/common/navbar/NavBar.vue'

export default {
  name : 'DetailItem',
  components : {
    NavBar
  },
  data () {
    return {
      titles : ['商品','参数','评论','推荐'],
      currentIndex : 0
    }
  },
  methods : {
    titleClick (index) {
      this.currentIndex = index
    },
    backClick () {
      this.$router.go(-1)
    }
  }
}
</script>

<style>
  .title {
    display: flex;
  }

  .title-item {
    flex: 1;
    font-size: 14px;
  }

  .active {
    color: var(---color-high-text);
  }

  .left-back {
    font-size: 20px;
  }
</style>