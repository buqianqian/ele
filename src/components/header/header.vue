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
    <transition name="fade">
      <div class="detail" v-show="showDetail">
        <div class="detail-wrapper clearfix">
          <div class="detail-main">
            <h1 class="name">{{seller.name}}</h1>
            <div class="star-wrapper">
              <Star :size="48" :score="seller.score"></Star>
            </div>
            <div class="title">
              <div class="line"></div>
              <div class="text">优惠信息</div>
              <div class="line"></div>
            </div>
            <ul v-if="seller.supports" class="supports">
              <li class="support-item" v-for="(item, index) in seller.supports" :key="index">
                <span class="icon" :class="classmap[item.type]"></span><span class="text">{{item.description}}</span>
              </li>
            </ul>
            <div class="title">
              <div class="line"></div>
              <div class="text">商家公告</div>
              <div class="line"></div>
            </div>
            <div class="bulletin">{{seller.bulletin}}</div>
          </div>
        </div>
        <div class="detail-close">
          <i class="icon-close" @click="closeDetail"></i>
        </div>
      </div>
    </transition>
  </div>
</template>

<script>
import Star from '@/components/star/star.vue'
export default {
  components: {
    Star
  },
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
    },
    closeDetail () {
      this.showDetail = false
    }
  }
}
</script>

<style lang="stylus" scoped>
@import '../../common/stylus/mixin'
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
            bg-image(decrease_1)
          }
          &.discount {
            bg-image(discount_1)
          }
          &.guarantee {
            bg-image(guarantee_1)
          }
          &.invoice {
            bg-image(invoice_1)
          }
          &.special {
            bg-image(special_1)
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
      letter-spacing 1px
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
    backdrop-filter blur(10px)
    transition all 0.5s
    &.fade-transition {
      opacity 1
      background rgba(7,17,27,.8)
    }
    &.fade-enter,&.fade-leave-to {
      opacity 0
      background rgba(7,17,27,0)
    }
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
        .star-wrapper {
          text-align center
          padding-top 16px
          padding-bottom 28px
        }
        .title {
          display flex
          width 80%
          // height 20px
          margin 0 auto
          .line {
            flex 1
            border-bottom 1px solid rgba(255,255,255,.2)
            position relative
            top -6px
          }
          .text {
            font-size 14px
            font-weight bold
            color #fff
            padding 0 10px
          }
        }
        .supports {
          padding 24px 48px
          .support-item {
            margin-bottom 12px
          }
          .text {
            font-size 12px
            color #fff
            line-height 12px
            margin-left 12px
          }
          .icon {
            display inline-block
            width 16px
            height 16px
            background-size 16px 16px
            vertical-align top
            &.decrease {
              bg-image(decrease_1)
            }
            &.discount {
              bg-image(discount_1)
            }
            &.guarantee {
              bg-image(guarantee_1)
            }
            &.invoice {
              bg-image(invoice_1)
            }
            &.special {
              bg-image(special_1)
            }
          }
        }
        .bulletin {
          color #fff
          font-size 12px
          line-height 24px
          padding 0 48px
          margin-top 24px
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
      color rgba(255,255,255,.5)
    }
  }
}
</style>
