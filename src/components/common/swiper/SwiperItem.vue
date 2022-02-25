<template>
  <div class="slide">
    <!-- 每一张图片 -->
    <slot></slot>   
  </div>
</template>

<script>
	export default {
		name: "SwiperItem"
	}
</script>

<style>
  .slide {
    width: 100%;
    flex-shrink: 0;
  }

  .slide img {
    width: 100%;
  }
</style>