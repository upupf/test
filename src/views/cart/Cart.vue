<template>
  <div id="cart">
    <nav-bar class="cart-nav">
      <div slot="center">购物车（）</div>
    </nav-bar>
  </div>
</template>

<script>
import NavBar from '@/components/common/navbar/NavBar.vue'

export default {
    name : 'Cart',
    components : {
      NavBar
    }
}
</script>

<style>
  .cart-nav {
    background-color: var(--color-tint);
  }
</style>