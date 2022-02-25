<template>
  <Swiper>
      <SwiperItem v-for="(item,index) in banner" :key="index">
        <a :href="item.link">
          <img :src="item.image" @load="imageLoad">
        </a>
      </SwiperItem>
    </Swiper>
</template>

<script>
import {Swiper, SwiperItem} from '@/components/common/swiper/index'


export default {
    name : 'HomeSwiper',
    props : {
        banner : {
            type : Array,
            default () {
                return []
            }
        }
    },
    data () {
      return {
        isLoad : false
      }
    },
    components : {
        Swiper,
        SwiperItem
    },
    methods : {
      imageLoad () {
        if(!this.isLoad) {
          this.$emit('swiperImageLoad')
          this.isLoad = true
        }
      }
    }
}
</script>

<style>

</style>