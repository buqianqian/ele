<template>
  <div class="goods">
    <div class="menu-wrapper" ref="menuWrapper">
      <ul>
        <li class="menu-item" :class="{'current': currentIndex === index}" v-for="(item,index) in goods" :key="index" @click="selectMenu(index)">
          <span class="text"><span class="icon" v-show="item.type>0" :class="classmap[item.type]"></span>{{item.name}}</span>
        </li>
      </ul>
    </div>
    <div class="foods-wrapper" ref="foodsWrapper">
      <ul>
        <li v-for="(item, index) in goods" :key="index" class="food-list-hook">
          <h1 class="menu">{{item.name}}</h1>
          <ul>
            <li v-for="(item, index) in item.foods" :key="index" class="food-item">
              <div class="icon">
                <img :src="item.icon" width="57">
              </div>
              <div class="content">
                <h2 class="name">{{item.name}}</h2>
                <p>{{item.description}}</p>
                <div class="extra">
                  <span>月售{{item.sellCount}}份</span><span style="margin-left: 12px">好评率{{item.rating}}%</span>
                </div>
                <div class="price">
                  <span style="font-size: 14px;color: rgb(147,153,159);font-weight: 700;color: red">￥{{item.price}}</span><span v-show="item.oldprice" style="font-size: 10px;font-weight: 700;color: rgb(147,153,159);margin-left:8px">￥{{item.oldprice}}</span>
                </div>
              </div>
            </li>
          </ul>
        </li>
      </ul>
    </div>
    <shopcar :delivery-price="seller.deliveryPrice" :min-price="seller.minPrice"></shopcar>
  </div>
</template>

<script>
import BScroll from 'better-scroll'
import shopcar from '@/components/shopcar/shopcar.vue'
export default {
  components: {
    shopcar
  },
  props: {
    seller: {
      type: Object
    }
  },
  data () {
    return {
      goods: [],
      classmap: [],
      listHeight: [],
      scrollY: 0
    }
  },
  created () {
    this.classmap = ['decrease', 'discount', 'guarantee', 'invoice', 'special']
    this.axios.get('/api/appData').then((body) => {
      if (body.data.errno === 0) {
        console.log(body.data.data.goods)
        this.goods = body.data.data.goods
        this.$nextTick(() => {
          this.initScroll()
          this.calcHeight()
        })
      }
    })
  },
  computed: {
    currentIndex () {
      for (let i = 0; i < this.listHeight.length; i++) {
        let height1 = this.listHeight[i]
        let height2 = this.listHeight[ i + 1 ]
        if (!height2 || (this.scrollY <= height2 && this.scrollY >= height1)) {
          return i
        }
      }
    }
  },
  methods: {
    initScroll () {
      this.menuScroll = new BScroll(this.$refs.menuWrapper, {
        click: true
      })
      this.foodsScroll = new BScroll(this.$refs.foodsWrapper, {
        probeType: 3
      })
      this.foodsScroll.on('scroll', (pos) => {
        this.scrollY = Math.abs(Math.round(pos.y))
      })
    },
    calcHeight () {
      let foodlist = this.$refs.foodsWrapper.getElementsByClassName('food-list-hook')
      let height = 0
      this.listHeight.push(height)
      for (let i = 0; i < foodlist.length; i++) {
        let item = foodlist[i]
        height += item.clientHeight
        this.listHeight.push(height)
      }
    },
    selectMenu (index) {
      // console.log(index)
      // console.log(this.listHeight[index])
      let foodlist = this.$refs.foodsWrapper.getElementsByClassName('food-list-hook')
      let el = foodlist[index + 1]
      this.foodsScroll.scrollToElement(el, 300)
    }
  }
}
</script>

<style lang="stylus" scoped>
@import '../../common/stylus/mixin'
.goods {
  touch-action none
  display flex
  width 100%
  position absolute
  top 177px
  left 0
  bottom 46px
  overflow scroll
  .menu-wrapper {
    flex 0 0 80px
    width 80px
    ul {
      .menu-item {
        background-color #f3f5f7
        width 80px
        height 54px
        line-height 14px
        font-size 12px
        display table
        border-bottom 1px solid rgba(7,17,27,.1)
        &.current {
          background-color #fff
          font-weight 700
          border none
        }
        .icon {
          display inline-block
          width 12px
          height 12px
          margin-right 4px
          background-size 12px 12px
          vertical-align top
          &.decrease {
            bg-image(decrease_3)
          }
          &.discount {
            bg-image(discount_3)
          }
          &.guarantee {
            bg-image(guarantee_3)
          }
          &.invoice {
            bg-image(invoice_3)
          }
          &.special {
            bg-image(special_3)
          }
        }
        .text {
          display table-cell
          vertical-align middle
          padding 0 12px
        }
      }
    }
  }
  .foods-wrapper {
    flex 1
    .menu {
      height 26px
      font-size 12px
      color rgb(147,153,159)
      line-height 26px
      border-left 2px solid #d9dde1
      padding-left 14px
      background-color #f3f5f7
    }
    .food-item {
      margin 0 18px
      margin-top 18px
      padding-bottom 18px
      display flex
      border-bottom 1px solid rgba(7,17,27,.1)
      &:last-child {
        border-bottom none
      }
      .icon {
        font-size 0
        display inline-block
        flex 0 0 57px
      }
      .content {
        display inline-block
        flex 1
        width 100%
        padding-left 10px
        .name {
          margin-top 2px
          font-size 14px
          color rgb(7,17,27)
        }
        p {
          font-size 10px
          color rgb(147,153,159)
          margin-top 8px
          line-height 10px
        }
        .extra {
          // display inline-block
          font-size 10px
          color rgb(147,153,159)
          margin-top 8px
        }
        .price {
          display inline-block
          margin-top 8px
        }
      }
    }
  }
}
</style>
