<template>
  <div id="app">
    <Carousel :images="slides"/>
  </div>
</template>

<script>
import Carousel from './components/Carousel.vue'

export default {
  name: 'app',
  components: {
    Carousel
  },
  data() {
    return {
      slides: [
        'https://undone.com/media/d/12884/Urban_modern_wht_front.png',
        'https://undone.com/media/d/12884/Urban_modern_wht_front.png',
        'https://undone.com/media/d/12884/Urban_modern_wht_front.png',
        'https://undone.com/media/d/12884/Urban_modern_wht_front.png',
        'https://undone.com/media/d/12884/Urban_modern_wht_front.png',
        'https://undone.com/media/d/12884/Urban_modern_wht_front.png',
        'https://undone.com/media/d/12884/Urban_modern_wht_front.png',
        'https://undone.com/media/d/12884/Urban_modern_wht_front.png',
        'https://undone.com/media/d/12884/Urban_modern_wht_front.png',
        'https://undone.com/media/d/12884/Urban_modern_wht_front.png',
        'https://undone.com/media/d/12884/Urban_modern_wht_front.png',
        'https://undone.com/media/d/12884/Urban_modern_wht_front.png'
      ]
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;

}
.item__image {
  width: 85%;
  -webkit-transform: translateX(10px) translateZ(0);
          transform: translateX(10px) translateZ(0); 
}
</style>
