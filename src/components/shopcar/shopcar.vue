<template>
  <div class="shopcar">
    <div class="content">
      <div class="content-left">
        <div class="logo-wrapper">
          <div class="logo" :class="{'highlight':totalCount > 0}">
            <span class="icon-shopping_cart"></span>
          </div>
          <div class="num" v-show="totalCount > 0">{{totalCount}}</div>
        </div>
        <div class="price" :class="{'highlight':totalCount > 0}">￥{{totalPrice}}</div>
        <div class="line"></div>
        <div class="desc">另需配送费￥{{deliveryPrice}}元</div>
      </div>
      <div class="content-right" :class="payClass">{{payDesc}}</div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    deliveryPrice: {
      type: Number,
      default: 0
    },
    minPrice: {
      type: Number,
      default: 0
    },
    selectFoods: {
      type: Array,
      default () {
        return [
          {
            price: 8,
            count: 2
          }
        ]
      }
    }
  },
  computed: {
    totalPrice () {
      let total = 0
      this.selectFoods.forEach(food => {
        total += food.price * food.count
      })
      return total
    },
    totalCount () {
      let count = 0
      this.selectFoods.forEach(food => {
        count += food.count
      })
      return count
    },
    payDesc () {
      if (this.totalPrice === 0) {
        return `￥${this.minPrice}元起送`
      } else if (this.totalPrice < this.minPrice) {
        let diff = this.minPrice - this.totalPrice
        return `还差￥${diff}元起送`
      } else {
        return '去结算'
      }
    },
    payClass () {
      if (this.totalPrice < this.minPrice) {
        return 'not-enough'
      } else {
        return 'enough'
      }
    }
  }
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
          &.highlight {
            background-color rgb(0,160,220)
            color #fff
          }
        }
        .num {
          width 24px
          height 16px
          position absolute
          background-color red
          top 0px
          right 0px
          border-radius 8px
          color #fff
          text-align center
          font-size 9px
          line-height 16px
          box-shadow 0 4px 8px 0 rgba(0,0,0,.4)
        }
      }
      .price {
        color rgba(255,255,255,.4)
        font-size 16px
        line-height 48px
        margin-left 80px
        &.highlight {
          color #fff
        }
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
      &.enough {
        background-color #00b43c
        color #fff
      }
    }
  }
}
</style>
