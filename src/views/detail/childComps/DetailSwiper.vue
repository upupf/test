<template>
  <div>
    <Swiper class="detail-swiper">
      <SwiperItem v-for="(item, index) in topImages" :key="index">
        <img :src='item'/>
      </SwiperItem>
    </Swiper>
    <div>
      {{detailDesc}}
    </div>
  </div>
</template>

<script>
import {Swiper, SwiperItem} from "@/components/common/swiper"
export default {
  name : 'DetailSwiper',
  components : {
    Swiper, 
    SwiperItem
  },
  props : {
    topImages : {
      type : Array,
      default () {
        return []
      }
    },
    detailDesc : {
      type : String,
      default : ''
    }
  }
}
</script>

<style>
  .detail-swiper {
    height: 300px;
    overflow: hidden;
  }
</style>