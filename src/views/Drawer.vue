<template>
  <div>
    <button @click="isOpen = !isOpen">
      My Profile
    </button>

    <!-- bind methods to js lifecycle hooks -->
    <!-- :css="false" tells Vue it doesn’t need to worry about handling the transition classes here since we’re relying on the JavaScript hooks instead -->
    <transition
      @before-enter="beforeEnter"
      @enter="enter"
      @leave="leave"
      :css="false"
    >
      <div v-if="isOpen" class="drawer">
        <img src="../assets/avatar.png" alt="avatar" />
        <div></div>
        <div></div>
        <div></div>
        <div></div>
      </div>
    </transition>
  </div>
</template>

<script>
import Velocity from 'velocity-animate'
export default {
  data() {
    return {
      isOpen: false
    }
  },
  methods: {
    //initial style of the drawer before it enters the interface
    beforeEnter(el) {
      el.style.opacity = 0
      el.style.width = '0em'
    },
    //set the styles we want the drawer to end up with when it enters
    enter(el, done) {
      Velocity(
        // element to animate
        el,
        // object with ending style that enter to
        { opacity: 1, width: '12em' },
        // object with rules to define transition’s duration, its easing function,
        // and handed it done, which is a method that will be run when the velocity animation is complete
        // (this lets Vue know this hook has completed, and it can move on to the next one in its lifecycle)
        { duration: 1000, easing: 'easeOutCubic', complete: done } //ease out cubic (start faster and end slower)
        //{ duration: 1000, easing: [100, 5], complete: done } //spring physics (100 is the amount of tension, 5 is the amount of friction for this spring function)
      )
    },
    //set the styles we want the drawer to transition to when it leaves our interface
    leave(el, done) {
      Velocity(
        el,
        { opacity: 0, width: '0em' },
        { duration: 500, easing: 'easeInCubic', complete: done }
      )
    }
  }
}
</script>

<style scoped>
img {
  height: 2.5em;
  width: 2.5em;
  border-radius: 50%;
}

.drawer {
  display: flex;
  flex-direction: column;
  align-items: center;
  height: 20em;
  width: 12em;
  border-radius: 1%;
  background-color: #e0e0e0;
  box-shadow: 0.08em 0.03em 0.4em #ababab;
  padding-top: 0.7em;
}

.drawer div {
  height: 3.5em;
  width: 95%;
  margin-top: 0.6em;
  background-color: #f0f0f0;
  border: 0.02em solid #ababab;
  border-radius: 1%;
}
</style>
