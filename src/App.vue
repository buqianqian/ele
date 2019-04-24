<template>
  <div id="app">
    <v-header :seller="seller"></v-header>
    <div class="tab">
      <div class="tab-item">
        <router-link to="/goods">商品</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/ratings">评价</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/sellers">商家</router-link>
      </div>
    </div>
    <router-view></router-view>
  </div>
</template>

<script>
import header from './components/header/header.vue'
export default {
  name: 'App',
  components: {
    'v-header': header
  },
  data () {
    return {
      seller: {}
    }
  },
  created () {
    this.axios.get('/api/appData').then((body) => {
      // console.log(body)
      if (body.data.errno === 0) {
        this.seller = body.data.data.seller
        console.log(this.seller)
      }
    })
  }
}
</script>

<style lang="stylus" scoped>
@import "./common/stylus/mixin.styl";
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  .tab {
    display: flex;
    width: 100%;
    height: 40px;
    line-height: 40px;
    border-bottom: 1px solid rgba(7, 17, 27, 0.1);
    .tab-item {
      flex: 1;
      text-align: center;
      & > a {
        color: rgb(77, 85, 93)
      }
      & .active {
        color: rgb(240, 20, 20)
      }
    }
  }
}
</style>
