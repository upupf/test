<template>
  <tab-bar>
    <tab-bar-item path="/home" activeColor="#1296db">
      <img slot="barimg" src="../../../assets/img/tabbar/home.png">
      <img slot="barimg-active" src="../../../assets/img/tabbar/home-active.png">
      <div slot="bartext">首页</div>
    </tab-bar-item>

    <tab-bar-item path="/category" activeColor="#1296db">
      <img slot="barimg" src="../../../assets/img/tabbar/category.png">
      <img slot="barimg-active" src="../../../assets/img/tabbar/category-active.png">
      <div slot="bartext">分类</div>
    </tab-bar-item>

    <tab-bar-item path="cart" activeColor="#1296db">
      <img slot="barimg" src="../../../assets/img/tabbar/cart.png">
      <img slot="barimg-active" src="../../../assets/img/tabbar/cart-active.png">
      <div slot="bartext">购物车</div>
    </tab-bar-item>

    <tab-bar-item path="/profile" activeColor="#1296db">
      <img slot="barimg" src="../../../assets/img/tabbar/profile.png">
      <img slot="barimg-active" src="../../../assets/img/tabbar/profile-active.png">
      <div slot="bartext">我的</div>
    </tab-bar-item>
  </tab-bar>
</template>

<script>
import TabBar from '@/components/common/tabbar/TabBar.vue'
import TabBarItem from '@/components/common/tabbar/TabBarItem.vue'

export default {
    name : 'MainTabBar',
    components : {
        TabBar,
        TabBarItem
    }
}
</script>

<style>

</style>