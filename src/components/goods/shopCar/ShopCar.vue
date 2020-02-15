<template>
  <div class="shop-car">
    <div class="content-wrapper">
      <div class="content-left">
        <div class="logo-wrapper">
          <div class="logo" :class="{'havefood': totalCountAndPrice.count>0}">
            <span class="icon-shopping_cart" ref="cartposition"></span>
          </div>
        </div>
        <div class="countIcon" v-show="totalCountAndPrice.count>0">{{totalCountAndPrice.count}}</div>
        <div
          class="price"
          :class="{'haveprice': totalCountAndPrice.price>0}"
        >￥{{totalCountAndPrice.price}}</div>
      </div>

      <div class="content-middle">另需配送费￥{{deliveryPrice}}元</div>

      <div
        class="content-right"
        :class="{'enough': totalCountAndPrice.price>=minPrice }"
      >{{payDesc}}</div>
    </div>

    <drop-animation :diffPos="diffPos"></drop-animation>
  </div>
</template>

<script>
import DropAnimation from "../../common/animation/DropAnimation";
export default {
  name: "ShopCar",
  data() {
    return {
      deliveryPrice: 4,
      minPrice: 20,
      diffPos: null
    };
  },
  components: {
    DropAnimation
  },
  props: {
    selectedFoods: Array,
    buttonDom: Object
  },
  watch: {
    buttonDom() {
      let diffx = Math.round(
        this.buttonDom.addButtonDomEle.getBoundingClientRect().x -
          this.$refs.cartposition.getBoundingClientRect().x
      );
      let diffy = Math.round(
        this.buttonDom.addButtonDomEle.getBoundingClientRect().y -
          this.$refs.cartposition.getBoundingClientRect().y
      );
      this.diffPos = { x: diffx, y: diffy };
    }
  },

  computed: {
    totalCountAndPrice() {
      let totalcount = 0;
      let totalprice = 0;
      this.selectedFoods.forEach(food => {
        totalcount += food.count;
        totalprice += food.count * food.price;
      });
      return { count: totalcount, price: totalprice };
    },

    payDesc() {
      if (this.totalCountAndPrice.price === 0) {
        return `￥${this.minPrice}起送`;
      } else if (this.totalCountAndPrice.price < this.minPrice) {
        let diff = this.minPrice - this.totalCountAndPrice.price;
        return `还差￥${diff}起送`;
      } else {
        return "去结算";
      }
    }
  }
};
</script>
<style lang='stylus' scoped>
.shop-car {
  position: fixed;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 1rem;
  z-index: 30;

  .content-wrapper {
    display: flex;
    font-size: 0;
    background: #141d27;

    .content-left {
      .logo-wrapper {
        display: inline-block;
        position: relative;
        top: -0.16rem;
        width: 0.9rem;
        height: 0.9rem;
        border-radius: 50%;
        margin-left: 0.2rem;
        padding: 0.14rem;
        background: #141d27;

        .logo {
          width: 100%;
          height: 100%;
          border-radius: 50%;
          background: rgba(50, 50, 50, 0.5);
          text-align: center;
          color: #80858a;

          .icon-shopping_cart {
            line-height: 0.9rem;
            font-size: 0.48rem;
          }

          &.havefood {
            background-color: rgb(8, 169, 220);
            color: #fff;
          }
        }
      }

      .countIcon {
        position: fixed;
        left: 0.8rem;
        bottom: 0.8rem;
        width: 0.24rem;
        height: 0.18rem;
        line-height: 0.18rem;
        padding: 0.08rem 0.12rem;
        border-radius: 50%;
        font-size: 0.2rem;
        text-align: center;
        background-color: red;
        color: #fff;
      }

      .price {
        display: inline-block;
        vertical-align: top;
        font-size: 0.3rem;
        font-weight: 700;
        line-height: 0.6rem;
        margin-top: 0.2rem;
        padding: 0 0.3rem 0 0.15rem;
        border-right: solid 0.01rem rgba(255, 255, 255, 0.2);
        color: rgba(255, 255, 255, 0.4);

        &.haveprice {
          color: #fff;
        }
      }
    }

    .content-middle {
      flex: 1;
      font-size: 0.28rem;
      line-height: 1rem;
      padding-left: 0.2rem;
      color: rgba(255, 255, 255, 0.4);
    }

    .content-right {
      flex: 0 0 2.2rem;
      font-size: 0.3rem;
      font-weight: 700;
      line-height: 1rem;
      text-align: center;
      color: rgba(255, 255, 255, 0.4);
      background-color: rgba(50, 50, 50, 0.5);
      border-left: solid 0.01rem rgba(255, 255, 255, 0.2);

      &.enough {
        color: #fff;
        background-color: #00b43c;
      }
    }
  }
}
</style>
