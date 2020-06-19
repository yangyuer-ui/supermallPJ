
<template>
     <div id="home">
         <nav-bar class="home-nav">
             <div slot="center">购物街</div>
         </nav-bar>
        <home-swiper :banners="banners"></home-swiper>
        <recommend-view :recommends="recommends"></recommend-view>
        <feature-view></feature-view>
        <tab-control class="tab-control" :titles="['流行','新款','精选']"
         @tabClick="tabClick" ></tab-control>
        <goods-list :goods="showGoods" ></goods-list>
    <ul>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
    </ul>
     </div>
</template>
<script>
import NavBar from '@/components/common/navbar/NavBar'
import TabControl from '@/components/content/tabControl/TabControl'
import GoodsList from '@/components/content/goods/GoodsList'

import HomeSwiper from './childComps/HomeSwiper'
import RecommendView from './childComps/RecommendView'
import FeatureView from './childComps/FeatureView'

import  {getHomeMultidata,getHomeGoods} from "@/network/home"

export default {
     name: "home",
     components:{
         HomeSwiper,
         RecommendView,
         FeatureView, 
         NavBar,
         TabControl,
         GoodsList
     },
     data(){
         return{
             banners: [],
             recommends: [],
             goods: {
                 'pop' :{page: 0, list: []},
                 'new' :{page: 0, list: []},
                 'sell' :{page: 0, list: []},
             },
             currentType: 'pop'
         }
     },
     created() {
         //1.请求多个数据
         this.getHomeMultidata();
         
         //请求商品数据
         this.getHomeGoods('pop');
         this.getHomeGoods('new');
         this.getHomeGoods('sell');
     },
     computed: {
         showGoods(){
             return this.goods[this.currentType].list;
         }
     },
     methods: {
         //时间监听的相关方法
         tabClick(index){
             switch(index){
                 case 0: 
                     this.currentType = 'pop'
                 break
                 case 1:
                     this.currentType = 'new'
                     break
                 case 2:
                     this.currentType = 'sell'
                     break
             }
 
            
         },



         //网络请求相关的方法
         getHomeMultidata(){
            getHomeMultidata().then(res =>{
              this.banners = res.data.banner.list;
              this.recommends = res.data.recommend.list;
         })
         },
         getHomeGoods(type){
             const page = this.goods[type].page + 1;
            getHomeGoods(type, page).then(res =>{
               this.goods[type].list.push(...res.data.list);
               this.goods[type].page += 1;
         })
         }
     }
}
</script>
<style scoped>
#home{
    padding-top: 44px;
}
.home-nav{
   background-color: pink;
   color: white;
   position: fixed;
   left: 0;
   right: 0;
   top: 0;
   z-index: 9;
}
.tab-control{
    /*在达到44px之前。他的属性默认为static，当达到44的时候会自动将数显更改为fixed*/
    position: sticky;
    top: 44px;
    z-index: 9;
}
</style>

