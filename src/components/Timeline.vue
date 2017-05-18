<template>
<transition name="fade">
   <div v-if="timeLineState" class="timeline_wapper">
      TIMELINE
   </div>
</transition>
</template>

<script>

export default {
  props: {
      timeLineState: {
        type: Boolean,
        default: false
      }
  },
}
</script>

<style scoped>
.timeline_wapper{
  height: 100vh;
  width: 100vw;
  background: rgba(0,0,0,.5);
  position: absolute;
  z-index: 8;
  top: 0
}


</style>
