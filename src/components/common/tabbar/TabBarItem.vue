<template>
  <div class="tab-bar-item" @click="itemClick">
      <!-- <div :style="activeStyle">
        <slot v-if="isActive" name="barimg-active"></slot>
        <slot v-else name="barimg"></slot>
        <slot name="bartext">首页</slot>
      </div> -->
      <div :style="activeStyle">
        <slot v-if="isActive" name="barimg-active"></slot>
        <slot v-else name="barimg"></slot>
        <slot name="bartext"></slot>
      </div>
  </div>
</template>

<script>
export default {
    name : 'TabBarItem',
    props : {
        path : String,
        activeColor : {
            type : String,
            default : 'red'
        }
    },
    computed : {
        isActive () {
            return this.$route.path.indexOf(this.path) !== -1
        },
        activeStyle () {
            return this.isActive ? {color : this.activeColor} : {}
        }
    },
    methods : {
        itemClick () {
            this.$router.replace(this.path).catch(err => {})
        }
    }
}
</script>

<style>
  .tab-bar-item {
    flex: 1;
    text-align: center;
    height: 49px;
    margin-top: 3px;
  }
  .tab-bar-item img {
    width: 24px;
    height: 24px;
  }
 
</style>