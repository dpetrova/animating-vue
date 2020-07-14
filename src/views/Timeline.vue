<template>
  <div>
    <img class="runner first" src="../assets/runner.png" alt="runner" />
    <img class="runner second" src="../assets/runner.png" alt="runner" />
    <img class="runner third" src="../assets/runner.png" alt="runner" />
  </div>
</template>

<script>
import gsap from 'gsap'

export default {
  mounted() {
    let tl = gsap.timeline({ repeat: -1, repeatDelay: 1 }) // timeline (loop indefinitely with delay of 1 seconds before next repetition)
    //tl.to('.first', { x: 700, duration: 2, ease: 'expo.out' }) //first runner
    //tl.to('.second', { x: 700, duration: 2, ease: 'expo.out' }, 0.5) //absolute position (will start 0.5 seconds into the sequence)
    //tl.to('.second', { x: 700, duration: 2, ease: 'expo.out' }, '-=1.45') //start of the tween 1.45 seconds before (-=) or after (+=) the end of the animation before it
    //tl.to('.third', { x: 700, duration: 2, ease: 'expo.out' }) //third runner
    tl.to('.first', { x: 700, duration: 2, ease: 'expo.out' })
    tl.to('.second', { x: 700, duration: 2, ease: 'expo.out' }, '<0.5') // start 0.5 seconds after the first starts
    tl.to('.third', { x: 700, duration: 2, ease: 'expo.out' }, '<') // starts when second tween starts
  }
}
</script>

<style scoped>
.runner {
  display: block;
  height: 5em;
  width: 5em;
  margin-top: 1.5em;
}
</style>