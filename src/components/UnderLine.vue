<template>
  <li>
  	<div class="under_text" @mouseover="hover" @mouseleave="out">{{text}}</div>
  	<transition name="fade">
    	<div v-if="lineShow" class="under_line" :style="{width: lineWidth + '%'}"></div>
  	</transition>
  </li>
</template>
<script>
export default {
  data () {
    return {
      lineShow: false,
      lineWidth: 0,
      timer: ""
    }
  },
  props: {
    text: {
      type: String,
      default: ''
    }
  },
  methods: {
      hover() {
        this.lineShow = true
        this.lineWidth = 0
        let self = this;
        this.timer = setInterval(function(){
        	if(self.lineWidth < 100){
        		self.lineWidth += 2
        	}else{
            clearInterval(self.timer)
          }
        },1)
      },
      out(){
      	this.lineShow = false
      	this.lineWidth = 0
      	clearInterval(this.timer)
      }
  }
}
</script>

<style scoped>
.under_text{
	cursor: pointer;
}
.under_line{
	height: 2px;
    background-color: white;
    margin-top: 8px;
}
.fade-enter-active, .fade-leave-active {
  	transition: opacity .5s;
}
.fade-enter, .fade-leave-active {
 	opacity: 0;
}
</style>
