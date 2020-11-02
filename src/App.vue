<template>
  <div id="app">
    <swiper :banners="banners"></swiper>
  </div>
</template>

<script>
import {request} from "./network/request";
import Swiper from "./components/Swiper";
export default {
  name: 'App',
  components: {
    Swiper
  },
  data(){
    return {
      banners:[],
    }
  },
  created() {
    request({
      url:'/home/multidata'
    }).then(res => {
      // console.log(res);
      this.banners = res.data.banner.list;
    });
  }
}
</script>
<style>
</style>
