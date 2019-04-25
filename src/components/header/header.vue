<template>
  <div class="header">
    <div class="content-wrapper">
      <div class="avatar">
        <img :src="seller.avatar" width="64" height="64">
      </div>
      <div class="content">
        <div class="title">
          <span class="brand"></span>
          <span class="name">{{seller.name}}</span>
        </div>
        <div class="description">
          {{seller.description}}/{{seller.deliveryTime}}分钟送达
        </div>
        <div class="support" v-if="seller.supports">
          <span class="icon" :class="classmap[seller.supports[0].type]"></span>
          <span class="text">
            {{seller.supports[0].description}}
          </span>
        </div>
        <div class="support-count" v-if="seller.supports" @click="showdetail">
          <span class="count">{{classmap.length}}个</span>
          <i class="icon-keyboard_arrow_right"></i>
        </div>
      </div>
    </div>
    <div class="bulletin-wrapper" @click="showdetail">
      <span class="bulletin-title"></span><span class="bulletin-text">{{seller.bulletin}}</span>
      <i class="icon-keyboard_arrow_right"></i>
    </div>
    <div class="background">
      <img :src="seller.avatar" width="100%" height="100%">
    </div>
    <div class="detail" v-show="showDetail">
      <div class="detail-wrapper clearfix">
        <div class="detail-main">
          <h1 class="name">{{seller.name}}</h1>
        </div>
      </div>
      <div class="detail-close">
        <i class="icon-close"></i>
      </div>
    </div>
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
      classmap: [],
      showDetail: false
    }
  },
  created () {
    console.log(this.seller)
    this.classmap = ['decrease', 'discount', 'guarantee', 'invoice', 'special']
  },
  methods: {
    showdetail () {
      this.showDetail = true
    }
  }
}
</script>

<style lang="stylus" scoped>
@import "../../common/stylus/mixin"
.header {
  position relative
  .content-wrapper {
    background-color rgba(7,17,27,.5)
    padding: 24px 12px 18px 24px;
    font-size: 0;
    position relative
    .avatar {
      display: inline-block;
      vertical-align top
      img {
        border-radius: 2px;
      }
    }
    .content {
      display: inline-block;
      font-size: 14px;
      margin-left: 16px;
      .title {
        margin 2px 0 8px 0
        .brand {
          display inline-block
          width 30px
          height 18px
          bg-image(brand)
          background-size 30px 18px
        }
        .name {
          font-size 16px
          color #fff
          font-weight bold
          line-height 18px
          vertical-align top
          margin-left 6px
        }
      }
      .description {
        font-size 12px
        font-weight 200
        color #fff
        margin-bottom 10px
      }
      .support {
        .icon {
          display inline-block
          width 12px
          height 12px
          margin-right 4px
          background-size 12px 12px
          vertical-align top
          &.decrease {
            bg-image('decrease_1')
          }
          &.discount {
            bg-image('discount_1')
          }
          &.guarantee {
            bg-image('guarantee_1')
          }
          &.invoice {
            bg-image('invoice_1')
          }
          &.special {
            bg-image('special_1')
          }
        }
        .text {
          color #fff
          font-size 10px
          vertical-align top
          display inline-block
          line-height 12px
        }
      }
      .support-count {
        background-color #fff
        position absolute
        right 12px
        bottom 18px
        padding 7px 8px
        background-color rgba(0,0,0,.2)
        color #fff
        font-size 10px
        border-radius 14px
        display inline-block
        .count {
          display inline-block
          margin-left 2px
          font-size 10px
          vertical-align top
        }
        .icon-keyboard_arrow_right {
          line-height 10px
        }
      }
    }
  }
  .bulletin-wrapper {
    height 28px
    background-color rgba(7,17,27,.2)
    padding 0 12px
    white-space nowrap
    overflow hidden
    text-overflow ellipsis
    font-size 10px
    color #fff
    line-height 28px
    position relative
    .bulletin-title {
      width 22px
      height 12px
      display inline-block
      background-size 22px 12px
      bg-image(bulletin)
      vertical-align middle
      margin-right 4px
    }
    .bulletin-text {
      margin-right 4px
    }
    .icon-keyboard_arrow_right {
      position absolute
      right 10px
      top 8px
      font-size 10px
      line-height 12px
    }
  }
  .background {
    width 100%
    height 100%
    position absolute
    top 0px
    left 0px
    z-index -1
    origin border-box
    filter blur(10px)
  }
  .detail {
    position fixed
    z-index 100
    overflow auto
    width 100%
    height 100%
    top 0px
    left 0px
    background rgba(7,17,27,.8)
    // filter blur(10px)
    .detail-wrapper {
      display inline-block
      width 100%
      min-height 100%
      .detail-main {
        margin-top 64px
        padding-bottom 64px
        .name {
          font-size 16px;
          color #fff
          text-align center
          font-weight 700
          line-height 16px
        }
      }
    }
    .detail-close {
      position relative
      width 32px
      height 32px
      margin -64px auto 0 auto
      clear both
      font-size 32px
    }
  }
}
</style>
