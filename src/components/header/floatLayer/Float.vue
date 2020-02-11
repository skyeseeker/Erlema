<template>
  <div class="float">
    <div class="wrapper clearfix">
      <div class="content">
        <p class="name">{{seller.name}}</p>
        <star class="star" :size="size" :score="score"></star>
        <div class="title">
          <div class="line"></div>
          <div class="text">优惠信息</div>
          <div class="line"></div>
        </div>

        <ul class="discountList" v-if="seller.supports">
          <li class="list" v-for="(item,index) in seller.supports" :key="index">
            <span class="icon" :class="classMap[item.type]"></span>
            {{item.description}}
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
    <div class="close-button">
      <span class="icon-close" @click="handleClose"></span>
    </div>
  </div>
</template>

<script>
import Star from "../../star/Star";
export default {
  name: "HeaderFloat",
  props: {
    seller: Object,
    classMap: Array
  },
  data() {
    return {
      size: 0.5,
      score: 4.3
    };
  },
  methods: {
    handleClose() {
      this.$emit("close");
    }
  },

  components: {
    Star
  }
};
</script>
<style lang='stylus' scoped>
.float {
  z-index: 100;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  overflow: auto;
  background: rgba(7, 17, 27, 0.8);
  color: #fff;

  .wrapper {
    min-height: 100%;
    width: 100%;

    .content {
      margin-top: 1.2rem;
      padding-bottom: 1rem;

      .name {
        line-height: 0.4rem;
        font-size: 0.4rem;
        font-weight: 600;
        text-align: center;
      }

      .star {
        text-align: center;
        margin-top: 0.36rem;
      }

      .title {
        display: flex;
        width: 80%;
        margin: 0.36rem auto 0.2rem auto;

        .line {
          flex: 1;
          position: relative;
          top: -0.17rem;
          border-bottom: 0.02rem solid rgba(255, 255, 255, 0.2);
        }

        .text {
          margin: 0 0.2rem;
          line-height: 0.34rem;
          font-size: 0.34rem;
          font-weight: 600;
        }
      }

      .discountList {
        margin-bottom: 0.3rem;

        .list {
          line-height: 0.3rem;
          font-size: 0.3rem;
          font-weight: 200;
          padding: 0.2rem 0 0 0.92rem;

          .icon {
            display: inline-block;
            vertical-align: middle;
            width: 0.4rem;
            height: 0.4rem;
            background-size: 100%;
            background-repeat: no-repeat;

            &.decrease {
              background-image: url('~img/decrease_1@2x.png');
            }

            &.discount {
              background-image: url('~img/discount_1@2x.png');
            }

            &.special {
              background-image: url('~img/special_1@2x.png');
            }

            &.invoice {
              background-image: url('~img/invoice_1@2x.png');
            }

            &.guarantee {
              background-image: url('~img/guarantee_1@2x.png');
            }
          }
        }
      }

      .bulletin {
        width: 76%;
        line-height: 0.6rem;
        font-size: 0.3rem;
        font-weight: 200;
        margin: 0.28rem auto 0 auto;
      }
    }
  }

  .close-button {
    position: relative;
    width: 0.6rem;
    height: 0.6rem;
    margin: -1rem auto 0 auto;
    clear: both;
    font-size: 0.6rem;
  }
}
</style>
