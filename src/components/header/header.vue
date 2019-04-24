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
          <span class="icon"></span>
          <span class="text">
            {{seller.supports[0].description}}
          </span>
        </div>
      </div>
    </div>
    <div class="bulletin-wrapper"></div>
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
    }
  },
  created () {
    console.log(this.seller)
  }
}
</script>

<style lang="stylus" scoped>
.header {
  .content-wrapper {
    background-color: rgba(0, 0, 0, .7);
    padding: 24px 12px 18px 24px;
    font-size: 0;
    .avatar {
      display: inline-block;
      border-radius: 2px;
    }
    .content {
      display: inline-block;
      font-size: 14px;
      margin-left: 16px;
      margin-top: 2px;
      .title {
        display inline-block;
        font-size: 16px;
        color: #fff;
        font-weight bold
        line-height 18px
      }
    }
  }
}
</style>
