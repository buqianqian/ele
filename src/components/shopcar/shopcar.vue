<template>
  <div class="shopcar">
    <div class="content">
      <div class="content-left">
        <div class="logo-wrapper">
          <div class="logo">
            <span class="icon-shopping_cart"></span>
          </div>
        </div>
        <div class="price">￥</div>
        <div class="line"></div>
        <div class="desc">另需配送费￥元</div>
      </div>
      <div class="content-right">￥起送</div>
    </div>
  </div>
</template>

<script>
export default {

}
</script>

<style lang="stylus" scoped>
.shopcar {
  position fixed
  left 0
  bottom 0
  z-index 50
  width 100%;
  height 48px
  background-color #141d27
  .content {
    height 100%
    display flex
    .content-left {
      // float left
      flex 1
      display flex
      height 100%
      .logo-wrapper {
        position fixed
        bottom 0
        left 12px
        width 58px
        height 58px
        background-color #141d27
        border-radius 50%
        .logo {
          width 44px
          height 44px
          background-color rgba(255,255,255,.2)
          border-radius 50%
          position absolute
          left 6px
          top 6px
          text-align center
          line-height 44px
          color rgba(255,255,255,.4)
          font-size 24px
        }
      }
      .price {
      color rgba(255,255,255,.4)
      font-size 16px
      line-height 48px
      margin-left 80px
      }
      .line {
        border-right 1px solid rgba(255,255,255,.1)
        margin-top 6px
        margin-left 12px
        margin-right 12px
        height 70%
      }
      .desc {
        font-size 14px
        font-weight 200
        line-height 48px
        color rgba(255,255,255,.4)
      }
    }
    .content-right {
      flex 0 0 105px
      color rgba(255,255,255,.4)
      background-color rgba(255,255,255,.1)
      text-align center
      line-height 48px
      font-size 14px
      font-weight 700
    }
  }
}
</style>
