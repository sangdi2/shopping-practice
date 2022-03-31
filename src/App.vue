<template>
  <div class="app-container">
    <Header></Header>
    <Goods v-for="item in list" :key="item.id" :title="item.goods_name"
    :pic="item.goods_img"
    :pirce="item.goods_price"
    :state="item.goods_state"
    :id="item.id"
    ></Goods>

  </div>
</template>

<script>
import Header from './components/Header/Header.vue'
import axios from 'axios'
import Goods from './components/Goods/Goods.vue'
export default {
  data(){
    return {
      list:[]
    }
  },
  methods:{
    async initcart(){
     const {data:res} =await axios.get('https://www.escook.cn/api/cart')
     console.log(res)
     if(res.status==200){
       this.list=res.list
     }
     }
  },
  created(){
     this.initcart()
  },
  components:{
    Header,
    Goods
  }
}
</script>

<style lang="less" scoped>
.app-container {
  padding-top: 45px;
  padding-bottom: 50px;
}
</style>
