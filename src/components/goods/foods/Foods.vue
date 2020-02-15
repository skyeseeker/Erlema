<template>
  <div class="wrapper" ref="Foodwrapper">
    <ul>
      <li class="item-wrapper" v-for="(item, index) in goodsData" :key="index" ref="itemWrapper">
        <div class="item-title">{{item.name}}</div>

        <ul>
          <li class="food-wrapper border-bottom" v-for="(food,index) in item.foods" :key="index">
            <div class="food-img-wrapper">
              <img class="food-img" :src="food.icon" />
            </div>

            <div class="food-content">
              <div class="food-name">{{food.name}}</div>
              <div class="food-description" v-show="food.description">{{food.description}}</div>
              <div class="extra">月售{{food.sellCount}}份&nbsp;&nbsp;&nbsp;好评率{{food.rating}}%</div>

              <div class="price">
                <span class="now">￥{{food.price}}</span>
                <span class="old" v-show="food.oldPrice">￥{{food.oldPrice}}</span>
              </div>
            </div>

            <span class="cartControl-wrapper">
              <cart-control :food="food" @deliverDom="handleDom"></cart-control>
            </span>
          </li>
        </ul>
      </li>
    </ul>
  </div>
</template>

<script>
import Bscroll from "better-scroll";
import CartControl from "../../common/cartControl/CartControl";
export default {
  name: "Foods",
  components: {
    CartControl,
  },
  data() {
    return {
      heightList: [],
      scrollY: 0,
      currentIndex: 0
    };
  },
  props: {
    goodsData: Array,
    selectedIndex: Number,
  },
  watch: {
    scrollY() {
      for (let i = 0; i < this.heightList.length; i++) {
        let start = this.heightList[i];
        let end = this.heightList[i + 1];
        if (!end || (this.scrollY >= start && this.scrollY < end)) {
          this.currentIndex = i;
          return;
        }
      }
    },
    currentIndex() {
      this.$emit("myIndex", this.currentIndex);
    },
    selectedIndex() {
      const element = this.$refs.itemWrapper[this.selectedIndex];
      this.foodsScroll.scrollToElement(element, 300);
    }
  },
  mounted() {
    this.createScrollAndHeightList();
    /**
      创建better-scroll实例和计算heightList都需要通过ref去绑定DOM元素，
    只有页面加载好，才能通过this.$refs获得。
      但是，如果使用了v-if v-show v-for等，即使在mounted阶段，页面也没
    有完全渲染好，无法取到DOM元素，会undefined。
      尝试在updated钩子函数中创建创建better-scroll实例和计算heightList，
    问题是，在子组件CartControl中，点击事件会给传过去的food对象添加count属性，
    此时，updated钩子函数会调用，就又会重复创建better-scroll实例。
      尝试使用this.$nextTick(() => {})，不行，不知道为什么
      使用延迟函数 setTimeout(() => {}, delaytime),有效
     */
  },
  methods: {
    handleDom(addButtonDomObj){
      this.$emit("deliverAddDom",addButtonDomObj)
    },
    createScrollAndHeightList() {
      setTimeout(() => {
        this.foodsScroll = new Bscroll(this.$refs.Foodwrapper, {
          click: true, //better-scroll 会阻止点击事件，配置 click:true ,会允许点击事件
          probeType: 3 //可以监听自己的滚动参数
        });
        this.foodsScroll.on("scroll", pos => {
          this.scrollY = Math.abs(Math.round(pos.y));
        });
        this.calculateHeightList();
      }, 300);
    },

    calculateHeightList() {
      for (let i = 0; i < this.goodsData.length; i++) {
        var height = this.$refs.itemWrapper[i].offsetTop;
        this.heightList.push(height);
      }
    }
  }
};
</script>

<style lang='stylus' scoped>
.border-bottom::before {
  border-bottom-color: rgba(7, 17, 27, 0.2);
  width: 94%;
  margin-left: 3%;
}

.wrapper {
  flex: 1;
  overflow: hidden;

  .item-wrapper {
    .item-title {
      height: 0.5rem;
      line-height: 0.5rem;
      border-left: 0.06rem solid #d9dde1;
      font-size: 0.27rem;
      padding-left: 0.14rem;
      color: rgb(147, 153, 159);
      background: #f3f5f7;
    }

    .food-wrapper {
      display: flex;
      padding: 3%;

      .food-img-wrapper {
        width: 1.3rem;
        height: 1.3rem;

        .food-img {
          width: 100%;
          height: 100%;
        }
      }

      .food-content {
        flex: 1;
        padding-left: 0.12rem;

        .food-name {
          font-size: 0.28rem;
          font-weight: 700;
          line-height: 0.28rem;
          padding-top: 0.04rem;
          padding-bottom: 0.12rem;
          color: rgb(7, 17, 27);
        }

        .food-description, .extra {
          font-size: 0.24rem;
          line-height: 0.24rem;
          padding-bottom: 0.1rem;
          font-weight: 100;
          color: rgb(147, 153, 159);
        }

        .price {
          .now {
            font-size: 0.3rem;
            font-weight: 700;
            color: rgb(240, 20, 20);
          }

          .old {
            text-decoration: line-through;
            font-size: 0.26rem;
            font-weight: normal;
            color: rgb(147, 153, 159);
          }
        }
      }

      .cartControl-wrapper {
        position: absolute;
        padding: 0;
        bottom: 0.12rem;
        right: 0.12rem;
      }
    }
  }
}
</style>
