<template>
  <div id="app">
    <main-tab-bar class="bar"></main-tab-bar>
   <router-view></router-view>
  </div>
</template>

<script>
import MainTabBar from '@/components/content/mainTabbar/MainTabBar'

export default {
  name: 'App',
  components: {
      MainTabBar,
  }
}
</script>

<style scoped>
     @import "~@/assets/css/base.css";
    
     .bar{
       z-index: 44;
     }
</style>
