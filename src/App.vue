<template lang="pug">
#app
  .people-list
    people(
      v-for="n in 32"
      :key="n"
      :num="n - 1"
      :direction="direction"
    )
  p
    button(@click="direction = 'up'") 上
    button(@click="direction = 'down'") 下
    button(@click="direction = 'left'") 左
    button(@click="direction = 'right'") 右
</template>

<script>
import People from './components/people'
export default {
  name: 'App',
  components: {
    People
  },
  data () {
    return {
      direction: 'down'
    }
  }
}
</script>

<style lang="less">
body {
  background-color: #c3e9fd;
}
.people-list {
  overflow: hidden;
}
</style>
