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
    var img = new Image()
    img.src=require('../assets/星星.png')
    onMounted(() => {
      const ctx2 = document.getElementById('starCanvas2').getContext('2d')

      // 主函数
      function Main(number) {
        let xyList = []
        let bList = []
        let countList=[]
        for (let i = 0; i < number; i++) {
          xyList.push({
            x: randomN(1000),
            y: randomN(600),
            r:randomN(10)
          })
          bList.push(randomN(6))
          countList.push(0)
        }
        setInterval(function () {
          ctx2.clearRect(0,0,1000,600)
          for (let i = 0; i < number; i++) {

            let b = bList[i]
            const xy = xyList[i]
            drawArc(ctx2, xy, b, xy.r)
            if (countList[i]>=12){
              bList[i]++
              countList[i]=0
            }
            if ( bList[i]===6){
               bList[i]=0
            }
            countList[i]++
          }
          // ctx2.save()
          // ctx2.globalCompositeOperation('destination-out')
          // ctx2.restore();
        }, 1000 / 60)
      }

      Main(50)
    })


    // 画点或圆函数
    function drawArc(ctx, classNumber, a, ra) {
      ctx.beginPath()
      ctx.drawImage(img,
          a*64,
          0,
          64,
          64,
          classNumber.x,
          classNumber.y,
          32/ra,
          32/ra)

      ctx.shadowColor = 'rgba(225,225,225,.8)';
      ctx.shadowBlur =20;
      ctx.shadowOffsetX = 0;
      ctx.shadowOffsetY = 0;
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