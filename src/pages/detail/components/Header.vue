<template>
    <div>
      <router-link to="../" v-show="show">
        <div class="iconfont back_icon">&#xe624;</div>
      </router-link>
      <div class="header" :style="opac" v-show="!show">
        {{sightTitle}}
        <router-link to="/">
          <div class="header_left">
            <div class="iconfont header_back_icon">&#xe624;</div>
          </div>
        </router-link>
      </div>
    </div>
</template>

<script>
export default {
  name: 'DetailHeader',
  props: {
    sightTitle: String
  },
  data () {
    return {
      show: true,
      opac: {
        opacity: 0
      }
    }
  },
  methods: {
    handleScroll () {
      let scrollTop = document.documentElement.scrollTop || window.pageYOffset || document.body.scrollTop
      // console.log(scrollTop)
      if (scrollTop > 40) {
        if (scrollTop < 210) {
          let tmp = scrollTop / 210
          this.opac.opacity = tmp // 动态样式的绑定
        }
        this.show = false
      } else {
        this.show = true
      }
    }
  },
  mounted () {
    window.addEventListener('scroll', this.handleScroll)
  },
  destroyed () {
    window.removeEventListener('scroll', this.handleScroll)
  }
}
</script>

<style lang="stylus" scoped>
@import '~styles/variable.styl'
  .back_icon
    position: absolute
    top: .08rem
    left: .1rem
    width: .72rem
    line-height: .72rem
    text-align: center
    border-radius: 100%
    background: rgba(0, 0, 0, .5)
    color: #fff
  .header
    position: fixed
    top: 0
    left: 0
    width: 100%
    height: $headerHeight
    line-height: $headerHeight
    background: $bgColor
    z-index: 2
    text-align: center
    font-size: .32rem
    color: #fff
    .header_left
      width: .64rem
      float: left
      color: #fff
      .header_back_icon
        text-align: center
        font-size: .4rem
</style>
