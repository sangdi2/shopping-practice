<template>
  <div class="number-container d-flex justify-content-center align-items-center">
    <!-- 减 1 的按钮 -->
    <button type="button" class="btn btn-light btn-sm" @click="sub">-</button>
    <!-- 购买的数量 -->
    <span class="number-box">{{amount}}</span>
    <!-- 加 1 的按钮 -->
    <button type="button" class="btn btn-light btn-sm" @click="add">+</button>
  </div>
</template>

<script>
import bus from '../eventBus.js'
export default {
  props:{
    amount:{
      default:1,
      Type:Number
    },
    id:{
      required:true,
      Type:Number
    }
  },
  methods:{
    add(){
      const obj={
        id:this.id,
        value:this.amount+1
      }
      bus.$emit('share',obj)
    },
    sub(){
      if(this.amount==0){
        return
      }
      const obj={
        id:this.id,
        value:this.amount-1
      }
      bus.$emit('sub',obj)
    }
  }
}
</script>

<style lang="less" scoped>
.number-box {
  min-width: 30px;
  text-align: center;
  margin: 0 5px;
  font-size: 12px;
}

.btn-sm {
  width: 30px;
}
</style>
