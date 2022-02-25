<template>
  <div>
    <detail-item/>
    <detail-swiper :topImages="topImages" :detailDesc="detailDesc"/>
  </div>
</template>

<script>
import DetailItem from './childComps/DetailItem.vue'
import DetailSwiper from './childComps/DetailSwiper.vue'

import {getDetail} from '@/network/detail.js'

export default {
  name : 'Detail',
  components : {
    DetailItem,
    DetailSwiper
  },
  data () {
    return {
      iid : null,
      topImages : [],
      detailDesc : ''
    }
  },
  created () {
    // 1.保存传入的iid
    this.iid  = this.$route.params.iid
    // console.log(this.iid);

    // 2.根据iid请求详情数据
    getDetail(this.iid).then(res => {
      // 1.获取顶部的图片轮播数据
      console.log(res.data.result);
      this.topImages = res.data.result.itemInfo.topImages
      this.detailDesc = res.data.result.itemInfo.desc
    })
  }
}
</script>

<style>

</style>