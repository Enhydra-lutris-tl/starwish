<template>
  <div class="main-back">
    <div>ceshi</div>
    <canvas height="600" width="1000" id="starCanvas"></canvas>
  </div>
</template>

<script>
import {onMounted} from "vue";

export default {
  name: "starCanvas",
  setup(){
    onMounted(()=>{
      const ctx = document.getElementById('starCanvas').getContext('2d')
      drawArc(ctx, 500, 300, 20, "rgb(76,145,232)", 1)
    })

    // 画点或圆函数
    function drawArc(ctx, x, y, r, color, fill){
      ctx.beginPath()
      ctx.fillStyle = color
      ctx.arc(x, y, r, 0, 2*Math.PI)
      if (fill){
        ctx.fill()
      }else {
        ctx.stroke()
      }
    }

    // 生成随机值
    // function random(){
    //
    // }






    return{

    }
   }
}
</script>

<style scoped>
.main-back{
  height: 100%;
  width: 100%;
}
canvas{
  border: #42b983 solid 2px;
}
</style>