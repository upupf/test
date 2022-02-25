<template>
  <div>
    <nav-bar class="category-nav">
      <div slot="center">分类栏</div>
    </nav-bar>
    <div class="wrapper" ref='aaa'></div>
   
      <div class="content"></div>
    <div/>
   
  </div>
</template>

<script>

import NavBar from '@/components/common/navbar/NavBar.vue'

import BScroll from 'better-scroll'

export default {
    name : 'Category',

    components : {
      NavBar
    },
    data () {
      return {
        scroll : null
      }
    },
    mounted () {
      // console.log(this.$refs.aaa);
      this.scroll = new BScroll (this.$refs.aaa, {
        probeType : 2,
        pullUpLoad : true
      })

      // this.scroll.on('scroll', (position) => {
      //   console.log(position);
      // })

      this.scroll.on('pullingUp', () => {
        console.log('上拉加载更多');
        setTimeout(() => {
          this.scroll.finishPullUp()
        }, 2000);
      })
    }
}
</script>

<style>
  .category-nav {
    background-color: var(--color-tint);
  }


  .wrapper {
    height: 150px;
    /* background-color: pink; */

    overflow: hidden;
    /* overflow-y: scroll; */
  }
</style>