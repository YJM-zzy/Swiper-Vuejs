<template>
  <div class="swiper">
    <!--      1、图片展示区域-->
    <div class="swiper-show">
        <div v-for="(item,index) in banners" :key="index" class="item-img" v-show="index === currentIndex-1">
          <a :href="item.link">
            <img :src="item.image" alt="">
          </a>
        </div>
    </div>
    <!--      2、指示器区域-->
    <div class="indicator">
        <div v-for="(item,index) in banners.length" :key="index" :class="{active:index===currentIndex-1}" @click="itemClick(index)"></div>
    </div>
  </div>
</template>

<script>
  export default {
    name: "Swiper",
    props:{
      banners:{
        type:Array,
        default(){
          return []
        }
      }
    },
    data(){
      return {
        currentIndex:1
      }
    },
    methods:{
      startTimer(){
        setInterval(() => {
          this.currentIndex++;
          if(this.currentIndex>this.banners.length){
            this.currentIndex = 1;
          }
        },2000)
      },
      stopTimer(){
        window.clearInterval(this.startTimer)
      },
      itemClick(index){
        this.stopTimer();
        this.currentIndex = index+1;
        // this.startTimer();
      }
    },
    created() {
      this.startTimer()
    }
  }
</script>

<style scoped>
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.swiper{
  overflow: hidden;
  position: relative;
  width: 600px;
  height: 300px;
}
.swiper-show{
  display: flex;
}
.item-img{
  width: 600px;
  height: 300px;
}
.item-img img{
  width: 100%;
  height: 100%;
}
.indicator {
  display: flex;
  justify-content: center;
  position: absolute;
  width: 100%;
  bottom: 8px;

}
.indicator div {
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background-color: #fff;
  line-height: 10px;
  text-align: center;
  font-size: 12px;
  margin: 0 5px;
}
.indicator .active{
  background-color: red;
}
</style>