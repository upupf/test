<template>
  <div class="back-top">
    <img src="../../../assets/img/common/top.png" alt="">
  </div>
</template>

<script>
  import BScroll from 'better-scroll'

  export default {
      name : 'BackTop',
      components : {
        
      },
      methods : {
        
      }
  }
</script>

<style>
  .back-top {
    position: fixed;
    right: 10px;
    bottom: 50px;
  }

  .back-top img {
    width: 43px;
    height: 43px;
  }
</style>