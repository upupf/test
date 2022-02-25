<template>
  <div id="home" class="wrapper" >
    <!-- 顶部导航 -->
    <NavBar class="home-nav"><div slot="center">首页</div></NavBar>  

     <!-- 控制转换栏 -->
    <TabControl :titles="['流行','新款','精选']"  @tabClick="tabClick"
                ref="tabControl1" class="tab-control"
                v-show="isTabFixed"></TabControl>

    
    <Bscroll class="content" ref="scroll" 
      :probe-type="3"  @scroll="contentScroll"
      :pull-up-load="true" @pullUpLoad="loadMore"> 
      <!-- 轮播图 -->
      <HomeSwiper :banner="banner" @swiperImageLoad="swiperImageLoad"></HomeSwiper>
      <!-- 推荐 -->
      <HomeRecommend :recommends="recommends"></HomeRecommend>
      <!-- 特性部分 -->
      <HomeFeature/>

      <!-- 控制转换栏 -->
      <TabControl :titles="['流行','新款','精选']"  @tabClick="tabClick"
                  ref="tabControl2"></TabControl>

      <!-- 商品展示 -->
      <GoodsList :goods="showGoods"></GoodsList>
    </Bscroll>

    <BackTop @click.native="backClick" v-show="isShowBackTop"></BackTop>

   
   

  </div>
</template>

<script>

import HomeSwiper from './childComps/HomeSwiper.vue'
import HomeRecommend from './childComps/HomeRecommend.vue'
import HomeFeature from './childComps/HomeFeature.vue'

import NavBar from '@/components/common/navbar/NavBar.vue'
import Bscroll from '@/components/common/scroll/Scroll.vue'

import TabControl from '@/components/content/tabControl/TabControl.vue'
import GoodsList from '@/components/content/goods/GoodsList.vue'
import BackTop from '@/components/content/backtop/BackTop.vue'


import {getHomeMultidata, getHomeGoods} from '@/network/home'
import {debounce} from '@/common/utils'


export default {
  name : 'Home',

  components : {
    HomeSwiper,
    HomeRecommend,
    HomeFeature,

    NavBar,
    Bscroll,
    TabControl,
    GoodsList,
    BackTop,

  },

  data () {
    return {
      banner : [],
      recommends : [],
      goods  : {
        'pop' : {page : 0, list : []},
        'new' : {page : 0, list : []},
        'sell' : {page : 0, list : []}
      },
      currentType : 'pop',
      isShowBackTop : false,
      tabOffsetTop : 0,
      isTabFixed : false,
      saveY : 0

    }
  },

  computed : {
    showGoods () {
      return this.goods[this.currentType].list
    },

   
  },

  created () {
    // 1.请求多个数据
    // getHomeMultidata().then(res => {
    //   console.log(res);
    //   this.banner = res.data.data.banner.list;
    //   this.recommends = res.data.data.recommend.list;
    // }),
    this.getHomeMultidata()

    /**
     *  2.请求商品数据
     */

    // getHomeGoods ('pop', 1).then(res => {
    //   console.log(res);
    // })
    this.getHomeGoods('pop')
    this.getHomeGoods('new')
    this.getHomeGoods('sell')

  },

  destroyed () {
    console.log('home destroyed');
  },

  activated () {
    this.$refs.scroll.scrollTo(0, this.saveY, 0)
    this.$refs.scroll.refresh()
  },

  deactivated () {
    this.saveY = this.$refs.scroll.scroll.y
    // console.log(this.saveY);
  },
  
  mounted () {
    
    const refresh = debounce(this.$refs.scroll.refresh, 300)

     /**
     * 1.监听item中图片加载完成
     */
    this.$bus.$on('itemImageLoad', () => {
      // console.log('-------');
      // this.$refs.scroll && this.$refs.scroll.refresh()
      this.$refs.scroll && refresh()
    })

    /**
     * 2.获取tabControl的offsetTop
     * 所有组件都有一个属性:$el ：用于获取组件中的元素
     * 此处是在生命周期mouted中实现，但是不能保证获取的offsetTop准确，
     * 因为可能上面图片并未加载完成，
     * 因此需要在轮播图加载完成再判断
     */
    // this.isTabControl = this.$refs()
    // setTimeout(() => {
    //   console.log(this.$refs.tabControl.$el.offsetTop);
    // },2000)
    
  },
  
  methods : {
    /**
     * 1.事件监听相关的方法
     */


    //  切换栏点击事件
    tabClick (index) {
      switch (index) {
        case 0 : 
          this.currentType  = 'pop';
          break;
        case 1 :
          this.currentType = 'new';
          break;
        case 2 : 
          this.currentType = 'sell';
          break;
      }
      this.$refs.tabControl1.currentIndex = index;
      this.$refs.tabControl2.currentIndex = index;
    },

    // 回到顶部点击事件
    backClick () {
      this.$refs.scroll.scrollTo(0, 0)
    },

    // 滚动位置监听事件
    contentScroll (position) {
      // console.log(-position.y);
      // 1.判断BackTop是否显示
      this.isShowBackTop = (-position.y) > 1000

      // 2.决定tabControl是否吸顶(position : fixed)
      this.isTabFixed = (-position.y) > this.tabOffsetTop
    },

    // 上拉加载更多监听事件
    loadMore () {

      this.getHomeGoods(this.currentType)

      //刷新
      // this.$refs.scroll.refresh()
    },

    // 轮播图加载监听事件
    swiperImageLoad () {
      this.tabOffsetTop = this.$refs.tabControl2.$el.offsetTop;
    },


    getScrollY() {
      return this.scroll ? this.scroll.y : 0
    },

    /**
     * 2.网络请求相关的方法
     */
    getHomeMultidata() {
      getHomeMultidata().then(res => {
        // console.log(res);
        this.banner = res.data.data.banner.list;
        this.recommends = res.data.data.recommend.list;
      })
    },
    getHomeGoods (type) {
      const page = this.goods[type].page + 1
      getHomeGoods (type, page).then(res => {
        // this.goods[type].list = res.
        this.goods[type].list.push(...res.data.data.list)
        this.goods[type].page += 1

        this.$refs.scroll.finishPullUp()
      })
    }


  }

}
</script>

<style scoped>
  #home {
    /* padding-top: 44px; */
    /* margin-top: 44px; */
    height: 100vh;
    position: relative;
  }
  .home-nav {
    background-color: var(--color-tint);
  }

  .tab-control {
    position: relative;
  }

  .content {
    overflow: hidden;
    position: absolute;
    top: 44px;
    bottom: 49px;
    left: 0;
    right: 0;
  }

  .fixed {
    position: fixed;
    left: 0;
    right: 0;
    top: 0;
  }

  /* .tab-control {
    position: sticky;
    top: 44px;
  } */

 
  /* .content {
    height: calc(100% - 52px);
    overflow: hidden;
  } */

</style>