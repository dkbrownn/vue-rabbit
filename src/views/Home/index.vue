<template>
  <div class="container">
    <HomeCategory/>
    <HomeBanner/>
    <HomeNew/>
    <HomeHot/>
    <HomeProduct/>
    
  </div>
</template>

<script setup lang='ts'>
import HomeCategory from './components/HomeCategory.vue'
import HomeBanner from './components/HomeBanner.vue'
import HomeNew from './components/HomeNew.vue'
import HomeHot from './components/HomeHot.vue'
import HomeProduct from './components/HomeProduct.vue' 
</script>
<style scoped>
.container{
  position: relative;
}
</style>