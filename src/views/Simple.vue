<template>
 <div>
   <!-- to work, the transition element that has animation should be placed into a wrapper (parent div) -->
  <transition appear @before-enter="beforeEnter" @enter="enter" :css="false">
    <div class="card"></div>    
  </transition>  
  </div>
</template>

<script>
import gsap from 'gsap'
export default {
  methods: {
    //define how card to be styled before it enters our interface
    beforeEnter(el) {
      el.style.opacity = 0 //invisible
      el.style.transform = 'scale(0,0)' //shrink of 0 for both x and y
    },
    //animate using gsap into a visible card at full scale
    enter(el, done) {
      //gsap.to(el, { duration: 3, opacity: 1, rotation: 360, scale: 0.5 })
      gsap.to(
        el, //which element to animate
        // an object that gives GSAP the styles for this element to end up with
        {
          duration: 1, //duration of 1 sec
          opacity: 1, //visible
          scale: 1, //scale to 100%
          ease: 'bounce.out',
          onComplete: done //lets Vue know that this step in the transition component’s lifecycle is complete, so Vue can move on to the next hook
        }
      )
    }
  }
}
</script>

<style scoped>
.card {
  display: block;
  margin: 0 auto 0 auto;
  height: 6.5em;
  width: 6.5em;
  border-radius: 5%;
  background-color: #16c0b0;
  box-shadow: 0.08em 0.03em 0.4em #ababab;
}
</style>
