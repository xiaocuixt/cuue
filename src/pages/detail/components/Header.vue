<template>
  <div>
    <router-link tag="div"
      to="/"
      class="header-abs"
      v-show="showAbs"
    >
      <span class="iconfont header-abs-icon">&#xe624;</span>
    </router-link>
    <div class="header-fixed"
      v-show="!showAbs"
      :style="opacityStyle">
      <router-link to="/">
        <span class="iconfont header-fixed-back">&#xe624;</span>
      </router-link>
      {{this.sightName}}
    </div>
  </div>
</template>

<script>
export default {
  name: 'DetailHeader',
  data () {
    return {
      showAbs: true,
      opacityStyle: {
        opacity: 0
      }
    }
  },
  props: {
    sightName: String
  },
  methods: {
    handleScroll () {
      const top = document.documentElement.scrollTop
      if (top > 60) {
        let opacity = top / 140
        opacity = opacity > 1 ? 1 : opacity

        this.opacityStyle = {
          opacity
        }
        this.showAbs = false
      } else {
        this.showAbs = true
      }
    }
  },
  activated () {
    window.addEventListener('scroll', this.handleScroll)
  },
  // 离开页面时对全局window时间进行解绑
  deactivated () {
    window.removeEventListener('scroll', this.handleScroll)
  }
}
</script>

<style lang="stylus" scoped>
  @import "~styles/variables.styl"

  .header-abs
    position: absolute
    text-align: center
    left: .2rem
    top: .2rem
    width: .8rem
    height: .8rem
    line-height: .8rem
    border-radius: .4rem
    background: rgba(0, 0, 0, .8)
    .header-abs-icon
      color: #fff
      font-size: .4rem
  .header-fixed
    z-index: 2
    position: fixed
    left: 0
    top: 0
    right: 0
    height: $headerHeight
    line-height: $headerHeight
    text-align: center
    background: $bgColor
    color: #fff
    font-size: .32rem
    .header-fixed-back
      position: absolute
      top: 0
      left: 0
      width: .64rem
      text-align: center
      font-size: .4rem
      color: #fff
</style>
