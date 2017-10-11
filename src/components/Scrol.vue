<template>
  <div ref="scroll">
    <slot></slot>
  </div>
</template>
<script>
  import BScroll from 'better-scroll'

  export default {
    props: {
      probeType: {
        type: Number,
        default: 1
      },
      click: {
        type: Boolean,
        default: true
      },
      pullup: {
        type: Boolean,
        default: false
      },
      pullDown: {
        type: Boolean,
        default: false
      },
      data: {
        type: Array,
        default: null
      },
      listenScroll: {
        type: Boolean,
        default: false
      },
    },
    data() {
      return {}
    },
    mounted() {
      setTimeout(() => {
        this.initScroll();
      }, 20)
    },
    methods: {
      initScroll() {
        this.scroll = new BScroll(this.$refs.scroll, {
          probeType: this.probeType,
          click: this.click
        })
        //如果监听滚动并派发事件 scroll
        if (this.listenScroll) {
          let that = this
          this.scroll.on('scroll', (pos) => {
            that.$emit('scroll', pos)
          })
        }
        //上拉加载
        if (this.pullup) {
          this.scroll.on('scrollEnd', (e) => {
            console.log(e)
            console.log(this.scroll.y)
            console.log(this.scroll.maxScrollY)
            if (this.scroll.y <= (this.scroll.maxScrollY + 100)) {
              this.$emit('scrollToEnd')
            }
          })
        }
        //下拉刷新
        if (this.pullDown) {
          this.scroll.on('scrollEnd', (e) => {
            console.log(e)
            console.log(this.scroll.y)
            console.log(this.scroll.maxScrollY)
            if (this.scroll.y >= (this.scroll.maxScrollY + 100)) {
              this.$emit('scrollToEnd')
            }
          })
        }

      },
      //重新渲染
      refresh() {
        this.scroll && this.scroll.refresh()
      },
      //滚动
      scrollToElement() {
        this.scroll && this.scroll.scrollToElement.apply(this.scroll, arguments)
      }
    },
    watch: {
      data() {
        setTimeout(() => {
          this.refresh()
        }, 20)
      }
    }
  }
</script>
<style scoped>

</style>
