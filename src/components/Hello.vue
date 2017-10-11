<template>
  <div class="hello">
    <div class="hd"></div>
    <div class="bd">
      <Scroll class="bd-inner"
              :data="liData"
              :pullup="pullup"
              :pullDown="pullDown"
              @scrollToEnd="loadMore"
      >
        <div>
          <ul>
            <div class="loading" v-show="hasMore">载入中…</div>
            <li v-for="(item,index) in liData">{{item}}</li>

          </ul>
        </div>

      </Scroll>
    </div>

  </div>
</template>

<script>
  import Scroll from './Scrol'

  export default {
    name: 'hello',
    data() {
      return {
        liData: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20],
        pullup: true,
        hasMore: false,
        pullDown: true
      }
    },
    components: {
      Scroll,
    },
    methods: {
      _ajax() {

        this.liData.push('新增数据' + Math.random())
        this.hasMore = false
      },
      loadMore() {
        this._ajax()
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .hd {
    width: 100%;
    height: 100px;
    background-color: #093;
  }

  .bd {
    width: 100%;
    position: fixed;
    top: 100px;
    bottom: 0;
  }

  .bd-inner {
    height: 100%;
    overflow: hidden;
  }

  ul li {
    text-align: center;
    line-height: 40px;
    border-bottom: 1px solid #eee;
  }

  .loading {
    width: 100%;
    text-align: center;
  }
</style>
