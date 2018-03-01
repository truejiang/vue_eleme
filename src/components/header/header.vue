<template>
  <div class="header">
    <div class="content-wrapper">
      <div class="avatar">
        <img width="64" height="64" :src="seller.avatar" alt="">
      </div>
      <div class="content">
        <div class="title">
          <span class="brand"></span>
          <span class="name">{{seller.name}}</span>
        </div>
        <div class="description">
          {{seller.description}}/{{seller.deliveryTime}}
        </div>
        <div @click="showDetail" class="support" v-if="seller.supports">
          <span class="icon" :class="classMap[seller.supports[0].type]"></span>
          <span class="text">{{seller.supports[0].description}}</span>
        </div>
      </div>
      <div @click="showDetail" v-if="seller.supports" class="support-count">
        <span class="count">{{seller.supports.length}}个</span>
        <i class="icon-keyboard_arrow_right"></i>
      </div>
    </div>
    <div class="bulletin-wrapper" @click="showDetail">
      <span class="bulletin-title"></span><span class="bulletin-text">{{seller.bulletin}}</span>
      <i class="icon-keyboard_arrow_right"></i>
    </div>
    <div class="background">
      <img :src="seller.avatar" alt="" width="100%" height="100%">
    </div>
    <!-- 公告详情 -->
    <transition>
      <div class="detail" v-show="detailShow">
        <div class="detail-wrapper clearfix">
          <div class="detail-main">
            <h1 class="name">{{seller.name}}</h1>
            <div class="star-wrapper">
              <star :size="48" :score="seller.score"></star>
            </div>
            <tit :msg="'优惠信息'"></tit>
            <ul v-if="seller.supports" class="supports">
              <li class="support-item" v-for="(item,index) in seller.supports" :key="index">
                <span class="icon" :class="classMap[item.type]" ></span>
                <span class="text">{{item.description}}</span>
              </li>
            </ul>
            <tit :msg="'商家公告'"></tit>
            <div class="bulletion">
              <p class="content">{{seller.bulletin}}</p>
            </div>
          </div>
        </div>
        <div class="detail-close" @click="showDetail">
          <i class="icon-close"></i>
        </div>
      </div>
    </transition>
  </div>
</template>
<script>
import star from '../common/star/star'
import tit from '../common/title/title'

export default {
  props: {
    seller: {
      type: Object
    },
    starType: {
      type: String
    }
  },
  data () {
    return {
      detailShow: false
    }
  },
  methods: {
    showDetail () {
      this.detailShow === true ? this.detailShow = false : this.detailShow = true
    }
  },
  created () {
    this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee']
  },
  components: {
    star: star,
    tit: tit
  }
}
</script>
<style lang="stylus">
@import '../../common/stylus/mixin';
.header
  color #ffffff
  position relative
  background-color rgba(7, 17, 27, 0.5)
  overflow hidden
  .content-wrapper
    padding 24px 12px 18px 24px
    font-size 0
    position relative
    .avatar
      display inline-block
      vertical-align top
      img
        border-radius 2px
    .content
      display inline-block
      margin-left 16px
      .title
        margin 2px 0 8px 0
        .brand
          display inline-block
          width 30px
          height 18px
          bg-image('brand')
          background-size 30px 18px
          background-repeat no-repeat
          vertical-align top
        .name
          margin-left 6px
          font-size 16px
          font-weight blod
          line-height 16px
      .description
        margin-bottom 10px
        line-height 12px
        font-size 12px
      .support
        .icon
          display inline-block
          width 12px
          height 12px
          margin-right 4px
          background-size 12px 12px
          background-repeat no-repeat
          vertical-align top
          &.decrease
            bg-image('decrease_1')
          &.discount
            bg-image('discount_1')
          &.guarantee
            bg-image('guarantee_1')
          &.invoice
            bg-image('invoice_1')
          &.special
            bg-image('special_1')
        .text
          line-height 12px
          font-size 10px
    .support-count
      position absolute
      right 12px
      bottom 14px
      padding  0 8px
      height 24px
      line-height 24px
      border-radius 14px
      background-color rgba(0, 0, 0, 0.2)
      text-align center
      .count
        font-size 10px
        vertical-align top
      .icon-keyboard_arrow_right
        height 24px
        margin-left 2px
        font-size 10px
        line-height 24px
  .bulletin-wrapper
    position relative
    height 28px
    line-height 28px
    padding 0 22px 0 12px
    white-space nowrap
    overflow hidden
    text-overflow ellipsis
    background-color rgba(7, 17, 27, 0.2)
    .bulletin-title
      display inline-block
      width 22px
      height 12px
      bg-image('bulletin')
      background-size 22px 12px
      background-repeat no-repeat
      vertical-align top
      margin-top 8px
    .bulletin-text
      font-size 10px
      margin 0 4px
      vertical-align top
    .icon-keyboard_arrow_right
        position absolute
        font-size 10px
        right 12px
        top 8px
  .background
    position absolute
    top 0
    left 0
    width 100%
    height 100%
    z-index -1
    filter blur(10px)
  .detail
    position fixed
    top 0
    left 0
    z-index 100
    width 100%
    height 100%
    overflow auto
    background-color rgba(7, 17, 27, 0.8)
    .fade-enter-active, .fade-leave-active
      transition all 0.5s
    &.fade-enter, &.fade-leave
      opacity 0
      background-color rgba(7, 17, 27, 0)
    .detail-wrapper
      min-height 100%
      width 100%
      .detail-main
        margin-top 64px
        padding-bottom 64px
        .name
          line-height 16px
          text-align center
          font-size 16px
          font-weight 700
        .star-wrapper
          margin-top 18px
          padding 2px 0
          text-align center
        .supports
          width calc(100% - 72px)
          margin 0 auto
          .support-item
            padding 0 12px
            margin-bottom 12px
            font-size 0
            &:last-child
              margin-bottom 0
            .icon
              display inline-block
              width 16px
              height 16px
              vertical-align top
              margin-right 16px
              background-size 16px 16px
              background-repeat no-repeat
              &.decrease
                bg-image('decrease_1')
              &.discount
                bg-image('discount_1')
              &.guarantee
                bg-image('guarantee_1')
              &.invoice
                bg-image('invoice_1')
              &.special
                bg-image('special_1')
            .text
              font-size 12px
              line-height 16px
              font-weight 200
              color rgb(255, 255, 255)
              vertical-align top
        .bulletion
          width calc(100% - 72px)
          margin 0 auto
          .content
            padding 0 12px
            font-size 12px
            font-weight 200
            color rgb(255, 255, 255)
            line-height 24px
    .detail-close
      position relative
      width 32px
      height 32px
      clear both
      margin -64px auto
      font-size 32px
</style>
