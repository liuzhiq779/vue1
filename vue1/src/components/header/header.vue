<template>
  <div class="header">
    <div class="content-wrapper">
      <div class="avatar">
        <img :src="seller.avatar">
      </div>
      <div class="content"> //内容
        <div class="title">
          <span class="brand"></span>
          <span class="name">{{seller.name}}</span>
        </div>
        <div class="description"> //描述
          {{seller.description}}/{{seller.deliveryTime}}分钟到达
        </div>
        <div class="support" v-if="seller.supports">
          <span class="icon" :class="classMap[seller.supports[0].type]"></span>
          <span class="text">{{seller.supports[0].description}}</span>
        </div>
      </div>
      <div class="supports_count" v-if="seller.supports" @click="showDetail(true)">
        <span class="count">{{seller.supports.length}}个</span>
        <span class="icon-keyboard_arrow_right"></span>
      </div>
    </div>
    <div class="bulletin-wrapper" @click="showDetail(true)">
      <span class="bulletin-title"></span>
      <span class="bulletin-text">{{seller.bulletin}}</span>
      <span class="icon-keyboard_arrow_right"></span>
    </div>
    <div class="background">
      <img :src="seller.avatar">
    </div>
    <transition name="fade">
      <div class="detail" v-show="detailShow">
        <div class="detail-wrapper">
          <div class="detail-main">
            <div class="name">{{seller.name}}</div>
            <div class="star-wrapper">
              <star :score="seller.score" :size="48"></star>
            </div>
            <div class="title">
              <div class="line"></div>
              <div class="text">优惠信息</div>
              <div class="line"></div>
            </div>
            <ul class="supports">
              <li class="support" v-for="support in seller.supports">
                <span class="icon" :class="classMap[support.type]"></span>
                <span class="text">{{support.description}}</span>
              </li>
            </ul>
            <div class="title">
              <div class="line"></div>
              <div class="text">商家公告</div>
              <div class="line"></div>
            </div>
            <div class="content">
              <p>{{seller.bulletin}}</p>
            </div>
          </div>
        </div>
        <div class="detail-close" @click="showDetail(false)">
          <span class="icon-close"></span>
        </div>
      </div>
    </transition>
  </div>
</template>

<script>
  import star from '../star/star.vue'
    export default {
    name: "header",
      props:['seller'],

      data () {
        return {
          detailShow: false
        }
      },

      created () {
        this.classMap = ["decrease","discount","guarantee","invoice","specical"]
      },

      methods: {
        showDetail (isShow) {
          this.detailShow = isShow
        }
      },

      component:{
      star
      }
    }
</script>

<style lang="stylus" rel="stylesheet/stylus" scoped>
 @import "../../common/stylus/mixins.styl"

  .header
    position relative
    background rgba(7,17,27,0.5)
    color white
    overflow hidden
    .content-wrapper
      position relative
      padding 24px 12px 18px 24px
      .avatar //头像
        vertical-align top
        display inline-block
        width 64px
        height 64px
        img
          width 100%
      .content
        display inline-block
        margin-left 16px
        padding 2px 0 2px
        .title
          .brand
            display inline-block
            width 30px
            height 18px
            background-repeat no-repeat
            background-size 30px 18px
            vertical-align middle
            bg-image(brand)
          .name
            margin-left 6px
            font-size 16px
            line-height 18px
            font-weight bold
        .description
          margin-top 8px
          margin-bottom 10px
          font-size 12px
          font-weight 200px
          line-height 12px
        .support
          .icon
            display inline-block
            width 12px
            height 12px
            background-size 12px 12px
            background-repeat no-repeat
            vertical-align middle
          .decrease
            bg-image(decrease_1)
          .discount
            bg-image(discount_1)
          .guarantee
            bg-image(guarantee_1)
          .invoice
            bg_image(invoice_1)
          .special




</style>
