<template >
    <canvas id = "shapes_wapper" > </canvas> 
</template>

<script >

    export default {
        data() {
            return {
                w: window.innerWidth || document.documentElement.clientWidth || document.body.clientWidth,
                h: window.innerHeight || document.documentElement.clientHeight || document.body.clientHeight,
                colorArry:['RGBA(184, 247, 136, .6)','RGBA(88, 210, 232, .6)','RGBA(244, 67, 54, .6)','RGBA(114, 109, 209, .6)','RGBA(230, 16, 155, .6)','RGBA(245, 164, 51, .6)','RGBA(0, 60, 255, .6)'],
                typeArry: ['cube', 'circle'],
            }
        },
        mounted() {
            let shapeCanvas = document.getElementById('shapes_wapper')
            let shapeContext = shapeCanvas.getContext('2d')
            shapeCanvas.height = this.h
            shapeCanvas.width = this.w
            
            let shapeOpts = {
              num:70,
              gatherRate:200,
              startX:[],
              startY:[],
              size:[],
              speed:[],
              color:[],
              type:[]
            }

            for (let i = 0; i < shapeOpts.num; i++) {
                let x_temp = this.rnd(0,this.w);
                let y_temp = x_temp / (this.w / this.h)
                shapeOpts.startX.push(x_temp);
                shapeOpts.startY.push(-y_temp);
                shapeOpts.size.push(this.rnd(15,30)) //半径
                shapeOpts.speed.push(this.rnd(4,5)) //速度
                shapeOpts.color.push(this.colorArry[this.rnd(0,this.colorArry.length - 1)]) //颜色
                shapeOpts.type.push(this.typeArry[this.rnd(0,this.typeArry.length - 1)]) //类型
            }

            let self = this;
            setInterval(function(){
              self.drawBackSnow(shapeContext,shapeOpts.startX,shapeOpts.startY,shapeOpts.num,shapeOpts.size,shapeOpts.gatherRate,shapeOpts.speed,shapeOpts.color,shapeOpts.type)
            },40);
        },
        methods: {
            rnd(n, m) {
                var random = Math.floor(Math.random() * (m - n + 1) + n);
                return random;
            },
            drawBackSnow(cxt, posX, posY, snows, snowSize, gatherRate, speed,color,type) {
                cxt.clearRect(0, 0, this.w, this.h);
                for (let i = 0; i < snows; i++) {
                    cxt.fillStyle = color[i];
                    
                    switch(type[i]){
                      case 'cube':
                        cxt.fillRect(posX[i],posY[i],snowSize[i]*2,snowSize[i]*2);
                        break;
                      case 'circle':
                        cxt.beginPath();
                        cxt.arc(posX[i], posY[i], snowSize[i], 0, 2 * Math.PI, true);
                        cxt.closePath()
                        cxt.fill();
                        break;
                    }
                    
                    posX[i] -= speed[i];
                    posY[i] += (this.h / this.w) * speed[i];
                    if (posX[i] < 0 || posY[i] > this.h) {
                        posX[i] = this.w + this.rnd(-gatherRate, 0);
                        posY[i] = this.rnd(-gatherRate, gatherRate);
                    }
                }
            }
        }
    } 
  </script>

<style >
    #shapes_wapper {
        position: absolute;
        top: 0
    }
    .shape {
        opacity: .9;
        position: absolute;
    }
    .cube {
        border - radius: 4 px;
    }
    .circle {
        border - radius: 50 % ;
    } 
</style>