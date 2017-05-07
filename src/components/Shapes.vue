<template>
 <div id="shapes_wapper"></div>
</template>

<script>
import Velocity from "../../static/velocity.min.js"

export default {
  data () {
    return {
      w:window.innerWidth || document.documentElement.clientWidth || document.body.clientWidth,
      h:window.innerHeight || document.documentElement.clientHeight || document.body.clientHeight,
      // colorArry:['#277E67','#673782','#9D5F28','#FFFF07','#F6323C','#F98CB8'],
      colorArry:['#fff','#fff','#fff','#fff','#cc0000'],
      typeArry:['cube','circle'],
      shapesWapper:'',
      shapesId:0
    }
  },
  mounted(){
    this.shapesWapper = document.getElementById('shapes_wapper')
    let self = this
    setInterval(function(){
      let startTop = self.rnd(-150,0)
      let startRight = self.rnd(-150,0)
      let height = self.rnd(20,40)
      let colorIndex = self.colorArry[self.rnd(0,self.colorArry.length - 1)]
      let rotateZ = self.rnd(-45,45) + 'deg'
      let shapeType = self.typeArry[self.rnd(0,self.typeArry.length - 1)]
      let speed = self.rnd(90,100)
      self.init(shapeType,colorIndex,startTop*2,startRight*2,height,rotateZ,speed)
    },1000)
  },
  methods: {
    rnd(n, m){
        var random = Math.floor(Math.random()*(m-n+1)+n);
        return random;
    },
    init(shapeType,background,top,right,height,rotateZ,speed){
      this.shapesWapper.insertAdjacentHTML('beforeend', '<div class="shape '+ shapeType +'" style="background:'+ background +';top:'+ top +'px;right:'+ right +'px;height:'+ height +'px;width:'+ height +'px" id="sid'+ this.shapesId +'"></div>')
      let sid_temp = "sid" + this.shapesId
      Velocity(document.getElementById(sid_temp), { top:this.h + top,right:this.w + Math.abs(right),rotateZ: rotateZ }, { duration: speed * 100,easing:'linear',complete: function(elements) { elements[0].parentNode.removeChild(elements[0])}})
      this.shapesId ++
    }
  }
}
</script>

<style>
.shape{
  opacity: .9;
  position: absolute;
}
.cube{
  border-radius: 4px;
}
.circle{
  border-radius: 50%;
}
</style>
