<template>
  <div class="title">
    <div class="line"></div>
    <div class="text">{{ msg }}</div>
    <div class="line"></div>
  </div>
</template>
<script>
export default {
  props: {
    msg: {
      type: String
    }
  }
}
</script>
<style lang="stylus" scoped>
.title
  display flex
  width calc(100% - 72px)
  margin 30px auto 24px auto
  .line
    flex: 1
    position relative
    top: -6px
    border-bottom 1px solid rgba(255, 255, 255, 0.2)
  .text
    padding 0 12px
    font-weight 700
    font-size 14px
</style>
