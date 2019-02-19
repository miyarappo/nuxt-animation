<template>
  <div class="TheButton">
    <div
      class="TheButton_Start"
      @click="click">
      <transition-group
        :css="false"
        tag="div"
        @enter="enter"
        @leave="leave"
      >
        <div
          v-if="!entered"
          key="start"
          class="TheButton_StartTitle">Click & Start
        </div>
        <div
          v-if="entered"
          key="return"
          class="TheButton_StartTitle">Click & Return
        </div>
      </transition-group>
      <div class="TheButton_StartUnderLine"/>
    </div>
  </div>
</template>

<script>
import { mapGetters, mapMutations } from 'vuex'
import { TweenMax, Expo } from 'gsap'

export default {
  computed: {
    ...mapGetters({
      entered: 'entered'
    })
  },
  methods: {
    enter(el, done) {
      TweenMax.to(el, 1.5, {
        opacity: 1,
        x: 0,
        startAt: {
          opacity: 0,
          x: '-20px'
        },
        ease: Expo.easeOut,
        onComplete: () => {
          done()
        }
      })
    },
    leave(el, done) {
      TweenMax.to(el, 1.5, {
        opacity: 0,
        x: '20px',
        startAt: {
          opacity: 1,
          x: 0
        },
        ease: Expo.easeOut,
        onComplete: () => {
          done()
        }
      })
    },
    ...mapMutations({
      click: 'click'
    })
  }
}
</script>

<style lang='scss' scoped>
.TheButton {
  display: flex;
  justify-content: center;
  position: relative;
  width: 100%;
  height: 40px;
  &_Start {
    position: relative;
    margin-top: 100px;
    width: 300px;
    height: 100%;
    font-size: 20px;
    letter-spacing: 2px;
    color: white;
    line-height: 2;
    text-align: center;
    cursor: pointer;
  }
  &_StartTitle {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    margin: auto;
  }
  &_StartUnderline {
    position: absolute;
    bottom: 0;
    width: 100%;
    height: 2px;
    background: #555;
  }
}
</style>
