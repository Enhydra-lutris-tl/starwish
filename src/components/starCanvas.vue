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
      // 旋转函数
      function rotateMain(number) {
        // let a = 0
        let rotateMsgList = []
        // let colorListBox = []
        let rList = []
        let aList = []
        let agLists = []
        for (let i = 0; i <number ; i++) {
          let r = randomN(8)
          if (r<4){
            r=4
          }
          let agr = randomN(2)
          if (agr===0){
            agr=1
          }
          rotateMsgList.push(getClass())
          // colorListBox.push({
          //   r: randomN(255),
          //   g: randomN(255),
          //   b: randomN(255),
          //   a: 1
          // })
          aList.push(0)
          rList.push(r)
          agLists.push(agr)

        }




        setInterval(function () {

          // ctx.clearRect(0, 0, 1000, 600)
          drawArc(ctx, {x: 500, y: 300}, 20, "rgb(76,145,232)", 1)
          for (let i = 0; i < number; i++) {
            const agList = agLists[i]
            let rotateMsg = rotateMsgList[i]
            // let colorList = colorListBox[i]
            const listColor = `rgb(255,255,255)`
            const classlist = getXY(rotateMsg)
            drawArc(ctx, classlist, Math.abs(rotateMsg.br)/30, listColor, 1)

            rotateMsg.ag+=agList
            if (rotateMsg.ag === 360) {
              rotateMsg.ag = 0
            }

            if (rotateMsg.br <= 20 && aList[i] === 0){
              aList[i] = 1
              rotateMsg.br +=0.1
            }else if (aList[i]===1 && rotateMsg.br >= 300){
              aList[i]=0
              rotateMsg.br -=0.1
            }else if(aList[i]===0 && rotateMsg.br <300){
              rotateMsg.br -=0.1
            }else if(aList[i]===1 && rotateMsg.br <300){
              rotateMsg.br +=0.1
            }
          }
          ctx.save()
          ctx.fillStyle = 'rgb(0, 0 , 0,.9)'
          ctx.globalCompositeOperation = 'destination-in';
          ctx.fillRect(0, 0, 1000, 600)
          ctx.restore();
          // a++
        }, 1000 / 60)
      }

      rotateMain(50)

      // 反推xy函数
      function getXY(classNumber) {
        let Tag, Tx, Ty
        if (classNumber.ag > 90 && classNumber.ag <= 180) {
          Tag = 180 - classNumber.ag
          Ty = classNumber.br * Math.cos(Tag * Math.PI / 180) * -1
          Tx = Ty * Math.tan(Tag * Math.PI / 180) * -1
        } else if (classNumber.ag > 180 && classNumber.ag <= 270) {
          Tag = classNumber.ag - 180
          Ty = classNumber.br * Math.cos(Tag * Math.PI / 180) * -1
          Tx = Ty * Math.tan(Tag * Math.PI / 180)
        } else if (classNumber.ag > 270 && classNumber.ag <= 360) {
          Tag = 360 - classNumber.ag
          Ty = classNumber.br * Math.cos(Tag * Math.PI / 180)
          Tx = Ty * Math.tan(Tag * Math.PI / 180) * -1
        } else {
          Tag = classNumber.ag
          Ty = classNumber.br * Math.cos(Tag * Math.PI / 180)
          Tx = Ty * Math.tan(Tag * Math.PI / 180)
        }
        const x = 500 + Tx
        const y = 300 - Ty
        return {
          Tag,
          Tx,
          Ty,
          x,
          y,
        }
      }
    })

    // 画点或圆函数
    function drawArc(ctx, classNumber, r, color, fill) {
      ctx.beginPath()
      ctx.fillStyle = color
      ctx.arc(classNumber.x, classNumber.y, r, 0, 2 * Math.PI)
      if (fill) {
        ctx.fill()
      } else {
        ctx.stroke()
      }
      ctx.shadowColor = 'rgba(225,225,225,.8)';
      ctx.shadowBlur =50;
      ctx.shadowOffsetX = 0;
      ctx.shadowOffsetY = 0;
    }

    // 生成随机值
    function randomN(number) {
      const Number = Math.random() * number
      return Math.round(Number)
    }

    // 生成所需字典方法
    function getClass() {
      let br = randomN(220)
      if (br<20){
        br=20
      }
      return {
        ag: randomN(360),
        br: br,
      }
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
  z-index: 10;
}

canvas {
  border: #42b983 solid 2px;
  /*background: rgba(0, 166, 255, 0.96);*/
}
</style>