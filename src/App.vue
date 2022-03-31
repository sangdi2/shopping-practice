<template>
  <div class="app-container">
    <Header></Header>
    <Goods v-for="item in list" :key="item.id" :title="item.goods_name"
    :pic="item.goods_img"
    :pirce="item.goods_price"
    :state="item.goods_state"
    :id="item.id"
    @getstate="getcheck"
    ></Goods>
     <Footer :isfull="isfull" @full="getfull"></Footer>
  </div>
</template>

<script>
import Header from './components/Header/Header.vue'
import axios from 'axios'
import Goods from './components/Goods/Goods.vue'
import Footer from './components/Footer/Footer.vue'
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
     },
     getcheck(val){
        console.log(val)
        this.list.some(item=>{
          if(item.id==val.id){
            console.log('ok')
            item.goods_state=val.value
          }
        })
     },
     getfull(v){
       this.list.forEach(item=>(item.goods_state=v))
     }
  },
  computed:{
    isfull(){
      return this.list.every(item=>(item.goods_state))
    }
  },
  created(){
     this.initcart()
  },
  components:{
    Header,
    Goods,
    Footer
  }
}
</script>

<style lang="less" scoped>
.app-container {
  padding-top: 45px;
  padding-bottom: 50px;
}
</style>
