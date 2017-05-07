<template>
<transition name="fade">
   <div v-if="loadingState" class="loading_wapper">
      <div class="ball-scale-ripple-multiple"><div></div><div></div><div></div></div>
   </div>
</transition>
</template>

<script>

export default {
  props: {
      loadingState: {
        type: Boolean,
        default: false
      }
  },
}
</script>

<style>
.loading_wapper{
  height: 100vh;
  width: 100vw;
  background: #141414;
  position: absolute;
  z-index: 100;
  top: 0
}
.fade-enter-active, .fade-leave-active {
  transition: opacity .5s
}
.fade-enter, .fade-leave-active {
  opacity: 0
}
.ball-scale-ripple-multiple {
  position: relative;
  -webkit-transform: translateY(-25px);
          transform: translateY(-25px); }
  .ball-scale-ripple-multiple > div:nth-child(0) {
    -webkit-animation-delay: -0.8s;
            animation-delay: -0.8s; }
  .ball-scale-ripple-multiple > div:nth-child(1) {
    -webkit-animation-delay: -0.6s;
            animation-delay: -0.6s; }
  .ball-scale-ripple-multiple > div:nth-child(2) {
    -webkit-animation-delay: -0.4s;
            animation-delay: -0.4s; }
  .ball-scale-ripple-multiple > div:nth-child(3) {
    -webkit-animation-delay: -0.2s;
            animation-delay: -0.2s; }
  .ball-scale-ripple-multiple > div {
    -webkit-animation-fill-mode: both;
            animation-fill-mode: both;
    position: absolute;
    top: 50vh;
    left: 50vw;
    margin-left: -25px;
    margin-top: -25px;
    width: 50px;
    height: 50px;
    border-radius: 100%;
    border: 2px solid #fff;
    -webkit-animation: ball-scale-ripple-multiple 1.25s 0s infinite cubic-bezier(0.21, 0.53, 0.56, 0.8);
            animation: ball-scale-ripple-multiple 1.25s 0s infinite cubic-bezier(0.21, 0.53, 0.56, 0.8); }

@keyframes ball-scale-ripple-multiple {
  0% {
    -webkit-transform: scale(0.1);
            transform: scale(0.1);
    opacity: 1; }
  70% {
    -webkit-transform: scale(1);
            transform: scale(1);
    opacity: 0.7; }
  100% {
    opacity: 0.0; } }
</style>
