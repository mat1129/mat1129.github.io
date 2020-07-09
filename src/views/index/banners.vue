<template>
  <div class="banner-warp">
    <swiper class="banner-inner" :options="swiperOption">
      <swiper-slide v-for="item in banners" :key="item.id">
        <router-link :to="'/app/home/productDetail/'+item.goods" target = _blank> <img :src="item.image" style="width: 1196px;height: 400px" alt="" /></router-link>
      </swiper-slide>
      <div class="swiper-pagination" slot="pagination"></div>
    </swiper>
  </div>
</template>
<style>
  .banner-warp{
    height:420px;
    width: 1196px;
    margin: 0 auto;
  }
  .banner-inner {
    /*margin-left: 214px;*/
  }
</style>



<script>
  import { swiper, swiperSlide } from 'vue-awesome-swiper'
  import {bannerGoods} from '../../api/api'

  export default {
    components: {
      swiper,
      swiperSlide,
    },
    data() {

      return {

        swiperOption: {
          pagination: '.swiper-pagination',
          paginationClickable: true,
          autoplay: 2500,
          autoplayDisableOnInteraction: false,
        },
        banners:[]

      }

    },
    methods:{
      getBanner(){
        bannerGoods()
          .then((response)=> {
            console.log(response)
            //跳转到首页页response.body面
            this.banners = response.data
          })
          .catch(function (error) {
            console.log(error);
          });
      }
    },
    created(){
      this.getBanner();
    }

  }

</script>
