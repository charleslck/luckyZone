<template>
  <section class="page_wapper">
    <div class="top_wapper clearfix">
      <div class="fl slogan_wapper">
        <h1>lucky zone</h1>
        <h2>关于陆晨凯</h2>
      </div>
      <div class="fr menu_wapper mr20 mt10">
        <ul>
           <UnderLine text='W·工作经验' @click.native="enent_w"></UnderLine>
           <UnderLine text='P·项目经验' @click.native="enent_p"></UnderLine>
           <UnderLine text='S·自我评价' @click.native="enent_s"></UnderLine>
        </ul>
      </div>
    </div>
    <div class="bottom_wapper">
      <JumpLine :data="indexShowTxt"></JumpLine>
    </div>
    <Shapes :colorData="colorArry"></Shapes>
    <Loading :loadingState="loadingState"></Loading>
  </section>
</template>

<script>

import UnderLine from './components/UnderLine'
import JumpLine from './components/JumpLine'
import Shapes from './components/ShapesCanvas'
import Loading from './components/Loading'

export default {
  data () {
    return {
      indexShowTxt: [{
        firstLine:"喜欢",
        secondLine:"迪丽热巴"
      },
      {
        firstLine:"精通",
        secondLine:"javascript"
      },
      {
        firstLine:"精通",
        secondLine:"vuejs jquery"
      },
      {
        firstLine:"熟练使用",
        secondLine:"agjs r-n r-web"
      },
      {
        firstLine:"掌握",
        secondLine:"reactjs"
      }],
      colorArry:['RGBA(184, 247, 136, .6)','RGBA(88, 210, 232, .6)','RGBA(244, 67, 54, .6)','RGBA(114, 109, 209, .6)','RGBA(230, 16, 155, .6)','RGBA(245, 164, 51, .6)','RGBA(0, 60, 255, .6)'],
      loadingState:true
    }
  },
  components: {
    UnderLine,
    JumpLine,
    Shapes,
    Loading
  },
  mounted(){
    let self = this
    setInterval(function(){
      self.loadingState = false
    },1000)
  },
  methods: {
    enent_w(){
      console.log('w')
    },
    enent_p(){
      console.log('p')
    },
    enent_s(){
      console.log('s')
    }
  }
}
</script>

<style scoped>
.top_wapper{
  position: relative;
  z-index: 10
}
.slogan_wapper{
  background: #141414
}
.slogan_wapper h1{
    color: white;
    text-transform: uppercase;
    letter-spacing: 3px;
    font-weight: 700;
    font-size: 3.5rem;
    margin: 15px 15px 5px 15px;
}
.slogan_wapper h2{
     color: white;
    letter-spacing: 35px;
    margin: 0 15px;
    font-size: 1.5rem;
    font-weight: normal;
}
.menu_wapper ul li{
  height: 50px;
  color: white;
  display: inline-block;
  font-size: 1.5rem;
  letter-spacing: 5px;
  text-indent: 5px;
  margin-left: 20px
}
.bottom_wapper{
  position: absolute;
  bottom: 20px;
  right: 30px;
  z-index: 10
}

</style>
