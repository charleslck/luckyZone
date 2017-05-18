<template>
  <div class="bottom">
 <!--    <div style="font-size:12px">
      <div v-if="!stopFlag" @click="stop">stop</div>
      <div v-if="stopState" @click="start">start</div>
    </div> -->
    <div>
      <div class="line_all line_one">
          <h3 :class="{ fadeIn: lineWidth.fadeInOne , fadeOut: !lineWidth.fadeInOne}" :style="{opacity: !lineWidth.fadeInOne?0:1}">{{lineWidth.textOne}}</h3>
          <div class="line" :style="{width: lineWidth.one + '%', float: lineWidth.oneDereciton}"></div>
      </div>
    </div>
    <div>
      <div class="line_all line_two">
        <h3 :class="{ fadeIn: lineWidth.fadeInTwo , fadeOut: !lineWidth.fadeInTwo}" :style="{opacity: !lineWidth.fadeInTwo?0:1}">{{lineWidth.textTwo}}</h3>
        <div class="line" :style="{width: lineWidth.two + '%', float: lineWidth.twoDereciton}"></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      lineWidth:{
        textOne :'姓名',
        one: 0,
        fadeInOne:false,
        oneDereciton: 'left',
        timerOne:{
          timerGoRight: '',
          timerGoLeft: ''
        },
        textTwo :"lu chen kai",
        two: 0,
        fadeInTwo:false,
        twoDereciton: 'left',
        timerTwo:{
          timerGoRight: '',
          timerGoLeft: ''
        },
        round:{
          one:0,
          two:0
        }
      },
      stopFlag:false,
      stopState:false,
      speed : 1,
      waitingTime: 0.9//seconds
    }
  },
  props: {
    data: {
      type: Array,
      default: []
    }
  },
  watch: {
    stopState: function (stopState) {
      if(stopState){
        let self = this
        let timer_temp = setTimeout(function(){
            self.start()
            clearTimeout(timer_temp)
        },self.waitingTime * 5000)
      }
    }
  },
  mounted(){
    let self = this
    setInterval(function(){
      self.stop()
      console.log("re")
    },20 * 1000)
    this.init(true)
  },
  methods: {
    start(){
      this.init(false)
    },
    stop(){
      this.stopFlag = true
    },
    init(firstRun){
      let self = this
      if(!firstRun){
        this.stopFlag = false
        this.stopState = false
      }
      let timer_temp_one = setTimeout(function(){
        self.jumpInOne()
        clearTimeout(timer_temp_one)
      },200)
      let timer_temp_two = setTimeout(function(){
         // self.jumpInOne()
        self.jumpInTwo()
        clearTimeout(timer_temp_two)
      },800)
    },
    jumpInOne(back){
      this.lineWidth.one = 0
      let self = this;
      this.lineWidth.timerOne.timerGoRight = setInterval(function(){
        if(self.lineWidth.one < 100){
          self.lineWidth.one += 2
        }else{
          clearInterval(self.lineWidth.timerOne.timerGoRight)
          let timer_temp_two = setTimeout(function(){
            if(back == 'back'){
              self.lineWidth.fadeInOne = false
              self.jumpOutOne('back')
            }else{
              self.lineWidth.fadeInOne = true
              self.jumpOutOne()
            }
            clearTimeout(timer_temp_two)
          },self.waitingTime * 1000)
        }
      },this.speed)
    },
    jumpOutOne(back){
      if(back == 'back'){
         this.lineWidth.oneDereciton = 'left'
      }else{
        this.lineWidth.oneDereciton = 'right'
      }
      let self = this;
      this.lineWidth.timerOne.timerGoLeft = setInterval(function(){
        if(self.lineWidth.one > 0){
          self.lineWidth.one -= 2
        }else{
          clearInterval(self.lineWidth.timerOne.timerGoLeft)
          if(back == 'back'){
                if(!self.stopFlag){
                   self.lineWidth.round.one ++
                   let timer_temp = setTimeout(function(){
                    self.changeData(1) 
                    self.lineWidth.fadeInOne = true
                    self.jumpInOne()
                    clearTimeout(timer_temp)
                  },self.waitingTime * 3000)
                 }else{
                   console.log('over1')
                 }
          }else{
            let timer_temp = setTimeout(function(){
              self.jumpInOne('back')
              clearTimeout(timer_temp)
            },self.waitingTime * 3000)
          }
        }
      },this.speed)
    },
    jumpInTwo(back){
      this.lineWidth.two = 0
      let self = this;
      this.lineWidth.timerTwo.timerGoRight = setInterval(function(){
        if(self.lineWidth.two < 100){
          self.lineWidth.two += 2
        }else{
          clearInterval(self.lineWidth.timerTwo.timerGoRight)
          let timer_temp_two = setTimeout(function(){
            if(back == 'back'){
              self.lineWidth.fadeInTwo = false
              self.jumpOutTwo('back')
            }else{
              self.lineWidth.fadeInTwo = true
              self.jumpOutTwo()
            }
            clearTimeout(timer_temp_two)
          },self.waitingTime * 1000)
        }
      },this.speed)
    },
    jumpOutTwo(back){
      if(back == 'back'){
         this.lineWidth.twoDereciton = 'left'
      }else{
        this.lineWidth.twoDereciton = 'right'
      }
      let self = this;
      this.lineWidth.timerTwo.timerGoLeft = setInterval(function(){
        if(self.lineWidth.two > 0){
          self.lineWidth.two -= 2
        }else{
          clearInterval(self.lineWidth.timerTwo.timerGoLeft)
          if(back == 'back'){
            if(!self.stopFlag){
               self.lineWidth.round.two ++
               let timer_temp = setTimeout(function(){
                self.changeData(2)  
                self.lineWidth.fadeInTwo = true
                self.jumpInTwo()
                clearTimeout(timer_temp)
              },self.waitingTime * 3000)
             }else{
              console.log('over2')
              self.stopState = true
             }
          }else{
            let timer_temp =  setTimeout(function(){
              self.jumpInTwo('back')
              clearTimeout(timer_temp)
            },self.waitingTime * 3000)
          }
        }
      },this.speed)
    },
    changeData(index){
      if(index == 1){
        let index_temp = this.lineWidth.round.one % this.data.length
        this.lineWidth.textOne = this.data[index_temp].firstLine
      }else{
        let index_temp = this.lineWidth.round.two % this.data.length
        this.lineWidth.textTwo = this.data[index_temp].secondLine
      }
    }
  }
}
</script>

<style scoped>
.bottom{
  color: white;
  text-align: right;
  font-size: 10rem
}
.line_all h3{
  margin: 0;
  text-transform: uppercase;
  font-weight: normal;
}
.line_all{
  letter-spacing: 10px;
  display: inline-block;
}
.line{
  background-color: white;
  height: 7px;
  margin-top: -15px
}
.fadeIn
{
  animation: fadeIn .6s;
  animation-delay: 0s;
  -moz-animation: fadeIn .6s; /* Firefox */
  -moz-animation-delay: 0s;
  -webkit-animation: fadeIn .6s;  /* Safari 和 Chrome */
  -webkit-animation-delay: 0s;
  -o-animation: fadeIn .6s; /* Opera */
  -o-animation-delay: 0s;
}
@keyframes fadeIn
{
  0% {transform: translateY(50px);opacity: 0}
  60% {transform: translateY(50px);opacity: 0}
  100% {transform: translateY(0px);opacity: 1}
}
.fadeOut
{
  animation: fadeOut .6s;
  animation-delay: 0s;
  -moz-animation: fadeOut .6s; /* Firefox */
  -moz-animation-delay: 0s;
  -webkit-animation: fadeOut .6s;  /* Safari 和 Chrome */
  -webkit-animation-delay: 0s;
  -o-animation: fadeOut .6s; /* Opera */
  -o-animation-delay: 0s;
}
@keyframes fadeOut
{
  0% {transform: translateY(0px);opacity: 1}
  60% {transform: translateY(50px);opacity: 0}
  100% {transform: translateY(50px);opacity: 0}
}
</style>
