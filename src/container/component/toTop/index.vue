<template>
    <div class="to-top-container" v-if="!isTop">
        <i class="el-icon-extend-back_to_top" @click="scrollToTop"></i>
    </div>
</template>
<script>
import './index.scss'
export default {
  name: 'ToTop',
  data () {
    return {
      isTop: true,
      timer: null
    }
  },
  mounted () {
    this.init()
  },
  methods: {
    init () {
      let $contentContainer = document.getElementById('main-content')
      $contentContainer.addEventListener('scroll', () => {
        this.isTop = $contentContainer.scrollTop < $contentContainer.offsetHeight / 5
      })
    },
    scrollToTop () {
      let $contentContainer = document.getElementById('main-content')
      this.timer = setInterval(() => {
        let scrollTop = $contentContainer.scrollTop
        if (scrollTop === 0) {
          clearInterval(this.timer)
          this.isTop = true
        } else {
          let speed = Math.floor(-scrollTop / 6)
          $contentContainer.scrollTop = scrollTop + speed
        }
      }, 20)
    }
  }
}
</script>
