<template>
  <div class="shopcart">
    <div class="content">
      <div class="content-left">
        <div class="logo-wrapper">
          <div class="logo">
            <i class="icon-shopping_cart"></i>
          </div>
        </div>
        <div class="price">￥0</div>
        <div class="desc">另需配送费￥{{deliveryPrice}}元</div>
      </div>
      <div class="content-right"></div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    deliveryPrice: {
      type: Number
    }
  }
}
</script>
<style lang="stylus" scoped>
  .shopcart
    position fixed
    bottom 0
    left 0
    z-index 99
    width 100%
    height 48px
    background-color #000
    .content
      display flex
      background-color #141d27
      font-size 0
      .content-left
        flex 1
        .logo-wrapper, .price, .desc
          display inline-block
        .logo-wrapper
          position relative
          top -10px
          margin 0 12px
          padding 6px
          width 56px
          height 56px
          box-sizing border-box
          vertical-align top
          border-radius 50%
          background-color #141d27
          .logo
            width 100%
            height 100%
            box-sizing border-box
            vertical-align top
            border-radius 50%
            background-color #2b343c
            text-align center
            .icon-shopping_cart
              line-height 44px
              font-size 24px
              color #80858a
        .price
          display inline-block
          font-size 24px
          vertical-align top
          line-height 24px
          margin-top 12px
          box-sizing border-box
          padding-right 12px
          border-right 1px solid rgba(255, 255, 255, 0.1)
          color rgba(255, 255, 255, 0.4)
        .desc
          display inline-block
          vertical-align top
          line-height 24px
          margin-left 12px
          margin-top 12px
          color rgba(255, 255, 255, 0.4)
          font-size 12px
      .content-right
        flex 0 0 105px
        width 105px
</style>
