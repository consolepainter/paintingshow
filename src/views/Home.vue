<template>
  <div class="home">
    <swiper></swiper>
  </div>
</template>

<script>
import Swiper from '../components/swiper/Swiper.vue';

export default {
  name: 'Home',
  components: {
    Swiper,
  }
}
</script>

<style scoped>
  .home {
    width: 100%;
    height: 100%;
  }
</style>
