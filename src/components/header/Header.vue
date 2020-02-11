<template>
  <div>
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
            <div class="support-exted" @click="handleFloat">
              {{seller.supports.length}}个
              <span class="icon-keyboard_arrow_right"></span>
            </div>
          </div>
        </div>
      </div>

      <div class="bulletin-wrapper" @click="handleFloat">
        <span class="bulletin-img"></span>
        {{seller.bulletin}}
        <span class="icon-keyboard_arrow_right"></span>
      </div>

      <div class="background">
        <img class="background-img" :src="seller.avatar" />
      </div>
    </div>

    <fade-animation>
      <header-float :seller="seller" :classMap="classMap" v-show="showFloat" @close="handleClose"></header-float>
    </fade-animation>
  </div>
</template>

<script>
import axios from "axios";
import HeaderFloat from "./floatLayer/Float";
import FadeAnimation from "../common/fade/FadeAnimation";
export default {
  name: "MyHeader",
  data() {
    return {
      showFloat: false,
      classMap: ["decrease", "discount", "special", "invoice", "guarantee"],
      seller: {}
    };
  },
  methods: {
    getSellerData() {
      axios
        .get("/api/seller")
        .then(this.getSellerDataSucc)
        .catch(err => {
          console.log(err);
        });
    },
    getSellerDataSucc(res) {
      const data = res.data;
      if (data.errno == 0 && data.data) {
        this.seller = data.data;
      }
    },
    handleFloat() {
      this.showFloat = true;
    },
    handleClose() {
      this.showFloat = false;
    }
  },
  created() {
    this.getSellerData();
  },
  components: {
    HeaderFloat,
    FadeAnimation
  }
};
</script>

<style lang='stylus' scoped>
@import '~style/mystyle.styl';

.header {
  position: relative;
  overflow: hidden;
  width: 100%;
  color: #fff;
  background: rgba(7, 17, 27, 0.5);

  .content-wrapper {
    display: flex;
    padding: 0.44rem 0 0.24rem 0.44rem;

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
      flex: 1;
      margin-left: 0.24rem;

      .title {
        margin: 0.04rem 0 0.18rem 0;
        line-height: 0.36rem;
        font-size: 0.34rem;
        font-weight: bold;

        .brand {
          display: inline-block;
          vertical-align: middle;
          width: 0.64rem;
          height: 0.4rem;
          background-image: url('~img/brand@2x.png');
          background-size: 100%;
          background-repeat: no-repeat;
        }
      }

      .desc {
        font-weight: 200;
        font-size: 0.3rem;
        margin-bottom: 0.18rem;
      }

      .support {
        margin-top: 0.04rem;
        font-size: 0.26rem;
        font-weight: 200;

        .icon {
          display: inline-block;
          vertical-align: middle;
          width: 0.3rem;
          height: 0.3rem;
          background-size: 100%;
          background-repeat: no-repeat;
          addDiscountClass();
        }

        .support-exted {
          position: absolute;
          top: 1.4rem;
          right: 0.2rem;
          height: 0.5rem;
          line-height: 0.5rem;
          width: 1rem;
          font-size: 0.26rem;
          text-align: center;
          border-radius: 0.6rem;
          background: rgba(0, 0, 0, 0.2);

          .icon-keyboard_arrow_right {
            vertical-align: middle;
            margin-left: -0.1rem;
            font-size: 0.3rem;
          }
        }
      }
    }
  }

  .bulletin-wrapper {
    position: relative;
    height: 0.6rem;
    line-height: 0.6rem;
    font-size: 0.21rem;
    font-weight: 100;
    padding-left: 0.2rem;
    padding-right: 0.32rem;
    letter-spacing: 0.02rem;
    ellipsis();
    background-color: rgba(7, 17, 27, 0.2);

    .bulletin-img {
      display: inline-block;
      vertical-align: middle;
      width: 0.5rem;
      height: 0.28rem;
      background-image: url('~img/bulletin@2x.png');
      background-size: 100%;
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
}
</style>
