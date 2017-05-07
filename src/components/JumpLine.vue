<template>
  <div class="bottom">
    <div>
    <div style="font-size:12px">
    </div>
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
        textOne :'welcome',
        one: 0,
        fadeInOne:false,
        oneDereciton: 'left',
        timerOne:{
          timerGoRight: '',
          timerGoLeft: ''
        },
        textTwo :" to lucky zone",
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
      speed : 1,
      waitingTime: 0.8//seconds
    }
  },
  props: {
    data: {
      type: Array,
      default: []
    }
  },
  mounted(){
    this.init()
  },
  methods: {
    init(){
      let self = this
      self.jumpInOne()
      setTimeout(function(){
        self.jumpInTwo()
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
          setTimeout(function(){
            if(back == 'back'){
              self.lineWidth.fadeInOne = false
            }else{
              self.lineWidth.fadeInOne = true
            }
          },self.waitingTime * 500)
          setTimeout(function(){
            if(back == 'back'){
              self.jumpOutOne('back')
            }else{
              self.jumpOutOne()
            }
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
             self.lineWidth.round.one ++   
             self.changeData(1)         
             setTimeout(function(){
              self.lineWidth.fadeInOne = true
              self.jumpInOne()
            },self.waitingTime * 3000)
          }else{
            setTimeout(function(){
              self.jumpInOne('back')
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
          setTimeout(function(){
            if(back == 'back'){
              self.lineWidth.fadeInTwo = false
            }else{
              self.lineWidth.fadeInTwo = true
            }
          },self.waitingTime * 500)
          setTimeout(function(){
            if(back == 'back'){
              self.jumpOutTwo('back')
            }else{
              self.jumpOutTwo()
            }
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
             self.lineWidth.round.two ++
             self.changeData(2)       
             setTimeout(function(){
              self.lineWidth.fadeInTwo = true
              self.jumpInTwo()
            },self.waitingTime * 3000)
          }else{
            setTimeout(function(){
              self.jumpInTwo('back')
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
