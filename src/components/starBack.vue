<template>
  <div class="main-back">
    <div>星球背景</div>
    <canvas height="600" width="1000" id="starCanvas2"></canvas>
  </div>
</template>

<script>
import {onMounted} from "vue";

export default {
  name: "starBack",
  setup() {
    onMounted(() => {
      const ctx2 = document.getElementById('starCanvas2').getContext('2d')

      // 主函数
      function Main(number) {
        let xyList = []
        for (let i = 0; i < number; i++) {
          xyList.push({
            x: randomN(1000),
            y: randomN(600),
            r:randomN(8)
          })
        }
        setInterval(function () {
          ctx2.clearRect(0,0,1000,600)
          for (let i = 0; i < number; i++) {
            const xy = xyList[i]
            drawArc(ctx2, xy, xy.r, 1)
          }
          // a++
        }, 1000 / 60)
      }

      Main(50)
    })


    // 画点或圆函数
    function drawArc(ctx, classNumber, r, fill) {
      ctx.beginPath()
      ctx.fillStyle = 'rgb(225,225,225)'
      ctx.arc(classNumber.x, classNumber.y, r, 0, 2 * Math.PI)
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

    return {}
  }
}
</script>

<style scoped>
.main-back {
  position: absolute;
  top: 0;
  left: 0;
  height: 100%;
  width: 100%;
  z-index: 2;
}

canvas {
  border: #42b983 solid 2px;
  background: black;
}
</style>