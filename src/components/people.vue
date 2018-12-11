<template lang="pug">
.people
  .people-content(:style="peopleStyle") {{ num }}
</template>

<script>
export default {
  props: {
    num: {
      type: Number,
      default: 0
    },
    speed: {
      type: Number,
      default: 100
    },
    direction: {
      type: String,
      default: 'down'
    }
  },
  data () {
    return {
      step: 0
    }
  },
  computed: {
    peopleStyle () {
      let style = {}
      let { step, num, direction } = this
      if (step === 3) step = 1
      let x = 0
      let y = 0
      let imageIndex = ~~(num / 8) + 1
      switch (num % 8) {
        case 1:
          x = 144
          break
        case 2:
          x = 288
          break
        case 3:
          x = 432
          break
        case 4:
          y = 192
          break
        case 5:
          y = 192
          x = 144
          break
        case 6:
          y = 192
          x = 288
          break
        case 7:
          y = 192
          x = 432
          break
      }
      switch (direction) {
        case 'up':
          y += 144
          break
        case 'left':
          y += 48
          break
        case 'right':
          y += 96
          break
      }
      style['background-position-x'] = -step * 48 - x + 'px'
      style['background-position-y'] = -y + 'px'
      style['background-image'] = `url(./static/images/people${imageIndex}.png)`
      return style
    }
  },
  mounted () {
    this.loop()
  },
  methods: {
    loop () {
      this.timer && clearTimeout(this.timer)
      this.timer = setTimeout(() => {
        this.addStep()
        this.loop()
      }, this.speed)
    },
    addStep () {
      let { step } = this
      step += 1
      if (step >= 4) step = 0
      this.step = step
    }
  }
}
</script>

<style lang="less">
.people {
  width: 48px;
  height: 48px;
  float: left;
  // animation-iteration-count: 3;
  .people-content {
    width: 100%;
    height: 100%;
    background-repeat: no-repeat;
  }
}
</style>
