<template>
  <div class="header">
    <div class="content-wrapper">
      <div class="avatar">
        <img class="avatar-img" :src="seller.avatar" />
      </div>

      <div class="content">
        <div class="title">
          <span class="brand"></span>
          {{seller.name}}
        </div>
        <div class="desc">{{seller.description}} / {{seller.deliveryTime}}分钟送达</div>
        <div class="support" v-if="seller.supports">
          <span class="icon" :class="classMap[seller.supports[0].type]"></span>
          {{seller.supports[0].description}}
          <div class="support-exted">
            {{seller.supports.length}}个
            <span class="icon-keyboard_arrow_right"></span>
          </div>
        </div>
      </div>
    </div>

    <div class="bulletin-wrapper">
      <span class="bulletin-img"></span>
      {{seller.bulletin}}
      <span class="icon-keyboard_arrow_right"></span>
    </div>

    <div class="background">
      <img class="background-img" :src="seller.avatar" />
    </div>
  </div>
</template>

<script>
export default {
  name: "MyHeader",
  data() {
    return {
      classMap: ["decrease", "discount", "special", "invoice", "guarantee"]
    };
  },
  props: { seller: Object },
  components: {}
};
</script>

<style lang='stylus' scoped>
.header {
  position: relative;
  width: 100%;
  height: 0;
  padding-bottom: 36%;
  color: #fff;
  background: rgba(7, 17, 27, 0.5);

  .content-wrapper {
    display: flex;
    padding: 0.44rem 0.24rem 0.24rem 0.44rem;

    .avatar {
      width: 20%;
      height: 0;
      padding-bottom: 20%;

      .avatar-img {
        width: 100%;
        border-radius: 0.04rem;
      }
    }

    .content {
      margin-left: 0.2rem;

      .title {
        margin: 0.02rem 0 0.18rem 0;
        line-height: 0.36rem;
        font-size: 0.34rem;
        font-weight: bold;

        .brand {
          display: inline-block;
          vertical-align: top;
          width: 0.64rem;
          height: 0.36rem;
          background-image: url('~img/brand@2x.png');
          background-size: 0.64rem 0.36rem;
          background-repeat: no-repeat;
        }
      }

      .desc {
        font-weight: 200;
        font-size: 0.3rem;
        margin-bottom: 0.18rem;
      }

      .support {
        position: relative;
        margin: 0.02rem 0 0.1rem 0;
        line-height: 0.3rem;
        font-size: 0.27rem;
        font-weight: 200;

        .icon {
          display: inline-block;
          vertical-align: top;
          width: 0.3rem;
          height: 0.3rem;
          background-size: 0.3rem 0.3rem;
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

        .support-exted {
          position: absolute;
          top: -0.1rem;
          right: -1.4rem;
          height: 0.5rem;
          line-height: 0.5rem;
          width: 1rem;
          font-size: 0.26rem;
          text-align: center;
          border-radius: 0.6rem;
          background: rgba(0, 0, 0, 0.2);

          .icon-keyboard_arrow_right {
            vertical-align: middle;
            margin-left: -0.08rem;
            font-size: 0.26rem;
          }
        }
      }
    }
  }
}

.bulletin-wrapper {
  position: relative;
  height: 0.6rem;
  line-height: 0.6rem;
  font-size: 0.2rem;
  font-weight: 100;
  padding-left: 0.2rem;
  padding-right: 0.32rem;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  background-color: rgba(7, 17, 27, 0.2);

  .bulletin-img {
    display: inline-block;
    vertical-align: middle;
    width: 0.5rem;
    height: 0.28rem;
    background-image: url('~img/bulletin@2x.png');
    background-size: 0.5rem 0.28rem;
    background-repeat: no-repeat;
  }

  .icon-keyboard_arrow_right {
    position: absolute;
    top: 0.16rem;
    right: 0.06rem;
    display: inline-block;
    vertical-align: middle;
    font-size: 0.3rem;
  }
}

.background {
  position: absolute;
  top: 0;
  left: 0;
  z-index: -1;
  width: 100%;
  height: 100%;
  filter: blur(10px);

  .background-img {
    width: 100%;
    height: 100%;
  }
}
</style>
