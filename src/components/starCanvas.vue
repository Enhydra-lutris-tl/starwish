<template>
  <div class="main-back">
    <div>星球运作</div>
    <canvas height="600" width="1000" id="starCanvas"></canvas>
  </div>
</template>

<script>
import {onMounted} from "vue";

export default {
  name: "starCanvas",
  setup() {
    onMounted(() => {
      const ctx = document.getElementById('starCanvas').getContext('2d')
      // const count = ref(0);
      drawArc(ctx, {x: 500, y: 300, r: 20, color: "rgb(76,145,232)"}, 1)
      const classNumber = getClass()
      const ceshishuju = {
        h: (classNumber.y - 300) * -1,
        w: classNumber.x - 500,
      }
      console.log(ceshishuju)
      const getMr = ceshishuju.h * ceshishuju.h + ceshishuju.w * ceshishuju.w
      const mr = Math.sqrt(getMr)

      // 求角度
      function getAg() {
        var ag = 0
        ag = Math.round(Math.atan(ceshishuju.w / ceshishuju.h) * 180 / Math.PI)
        if (ceshishuju.h < 0 && ceshishuju.w > 0) {
          ag = 180 + ag
        } else if (ceshishuju.h < 0 && ceshishuju.w < 0) {
          ag = 180 + ag
        } else if (ceshishuju.h > 0 && ceshishuju.w < 0) {
          ag = 360 + ag
        }
        return ag
      }
      console.log(mr, getAg())

      // 角度增长函数
      function ceshi2(mr, ag){
        const sin = Math.cos(ag*Math.PI/180)

      }
      drawArc(ctx, classNumber, 1)
      // const a = setInterval(function () {
      //   ctx.clearRect(0, 0, 1000, 600)
      //   drawArc(ctx, {x: 500, y: 300, r: 20, color: "rgb(76,145,232)"}, 1)
      //   for (let i = 0; i < 10; i++) {
      //     drawArc(ctx, getClass(), 1)
      //   }
      //   count.value++
      //   if (count.value === 100) {
      //     clearInterval(a)
      //   }
      // }, 1000 / 60)

    })

    // 画点或圆函数
    function drawArc(ctx, classNumber, fill) {
      ctx.beginPath()
      ctx.fillStyle = classNumber.color
      ctx.arc(classNumber.x, classNumber.y, classNumber.r, 0, 2 * Math.PI)
      if (fill) {
        ctx.fill()
      } else {
        ctx.stroke()
      }
    }

    // 生成随机值
    function randomN(number) {
      const Number = Math.random() * number

      return Math.round(Number)
    }

    // 生成所需字典方法
    function getClass() {
      return {
        x: randomN(1000),
        y: randomN(600),
        r: randomN(10),
        color: `rgb(${randomN(255)}, ${randomN(255)}, ${randomN(255)})`
      }
    }

    console.log(getClass())

    return {}
  }
}
</script>

<style scoped>
.main-back {
  height: 100%;
  width: 100%;
}

canvas {
  border: #42b983 solid 2px;
}
</style>