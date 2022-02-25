<template>
  <div>
    <nav-bar class="profile-nav">
      <div slot="center">我的</div>
    </nav-bar>

    <div class="wrapper" ref="bbb">
      <div class="content"></div>
    </div>
    <h2>我的</h2>
  </div>
</template>

<script>
import NavBar from '@/components/common/navbar/NavBar.vue'
import Bscroll from 'better-scroll'

export default {
    name : 'Profile',
    components : {
      NavBar
    },
    data () {
      return {
        bs : null
      }
    },
    mounted () {
      this.bs = new Bscroll (this.$refs.bbb, {

      })
    }
}
</script>

<style>
  .profile-nav {
    background-color: var(--color-tint);
  }

  .wrapper {
    height: 100px;
    /* background-color: pink; */

    overflow: hidden;
  }
</style>