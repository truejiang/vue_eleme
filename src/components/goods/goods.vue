<template>
  <div class="goods">
    <div class="menu-wrapper">
      <ul class="menu-ul">
        <li v-for="(item,index) in goods" :key="index" class="menu-item">
          <span class="text border-1px">
            <span v-show="item.type > 0" class="icon" :class="classMap[item.type]"></span>{{item.name}}
          </span>
        </li>
      </ul>
    </div>
    <div class="foods-wrapper"></div>
  </div>
</template>
<script>
export default {
  props: {
    seller: {
      type: Object
    }
  },
  data () {
    return {
      goods: {}
    }
  },
  created () {
    this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee']

    this.$axios.get('/api/goods').then((response) => {
      this.goods = response.data.data
    }).catch((err) => {
      console.log(err)
    })
  }
}
</script>
<style lang="stylus" scoped>
  @import '../../common/stylus/mixin'
  .goods
    display flex
    position absolute
    top 174px
    bottom 46px
    width 100%
    overflow hidden
    .menu-wrapper
      flex 0 0 80px
      width 80px
      background-color #f3f5f7
      .menu-ul
        width 100%
        .menu-item
          display table
          width 56px
          height 54px
          line-height 14px
          padding 0 12px
          .icon
            display inline-block
            width 16px
            height 16px
            vertical-align top
            margin-right 4px
            background-size 16px 16px
            background-repeat no-repeat
            &.decrease
              bg-image('decrease_3')
            &.discount
              bg-image('discount_3')
            &.guarantee
              bg-image('guarantee_3')
            &.invoice
              bg-image('invoice_3')
            &.special
              bg-image('special_3')
          .text
            display table-cell
            width 56px
            vertical-align middle
            font-size 12px
            border-1px(rgba(7, 17, 27, 0.1))
            line-height 16px
          &.active
            background-color #fff
    .foods-wrapper
      background-color #fff
</style>
