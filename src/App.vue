<template>
  <div id="app">
    <!-- <img src="./assets/logo.png"> -->
    <v-header :seller="seller"></v-header>
    <div class="tab border-1px">
      <router-link to="/goods" class="tab-item" tab="div">商品</router-link>
      <router-link to="/ratings" class="tab-item" tab="div">评论</router-link>
      <router-link to="/seller" class="tab-item" tab="div">商家</router-link>
    </div>
    <router-view :seller="seller"></router-view>
  </div>
</template>

<script>

import vHeader from './components/header/header.vue'
// import axios from 'axios'

export default {
  data () {
    return {
      seller: {}
    }
  },
  created () {
    this.$axios.get('/api/seller').then((response) => {
      this.seller = response.data.data
    }).catch((err) => {
      console.log(err)
    })
  },
  components: {
    vHeader: vHeader
  }
}
</script>

<style lang="stylus">
@import './common/stylus/mixin.styl';
#app
 .tab
   display flex
   width 100%
   height 40px
   line-height 40px
   border-1px(rgba(7, 17, 27, 0.1))
   .tab-item
     flex 1
     text-align center
     color black
     font-size 14px
     color rgb(77, 85, 93)
     &.active
      color rgb(240, 20, 20)
</style>
