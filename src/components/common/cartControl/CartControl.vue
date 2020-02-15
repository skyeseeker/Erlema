<template>
  <div class="cart">
    <move-animation>
      <div
        class="cart-minus icon-remove_circle_outline"
        v-show="this.food.count>0"
        @click="minusItem"
      ></div>
    </move-animation>

    <div class="cart-count" v-show="this.food.count>0">{{this.food.count}}</div>

    <div class="cart-add icon-add_circle" @click="addItem"></div>
  </div>
</template>

<script>
import Vue from "vue";
import MoveAnimation from "../animation/MoveAnimation";
export default {
  name: "CartControl",
  data() {
    return {};
  },
  components: {
    MoveAnimation
  },
  props: {
    food: Object
  },

  methods: {
    addItem(e) {
      if (!this.food.count) {
        Vue.set(this.food, "count", 1);
      } else {
        this.food.count++;
      }
      let buttonDom = { addButtonDomEle: e.target };
      this.$emit("deliverDom", buttonDom);
    },
    minusItem() {
      if (this.food.count) {
        this.food.count--;
      }
    }
  }
};
</script>



<style lang='stylus' scoped>
.cart {
  .cart-minus {
    display: inline-block;
    padding: 0.02rem;
    font-size: 0.36rem;
    line-height: 0.36rem;
    color: rgb(0, 160, 220);
  }

  .cart-count {
    display: inline-block;
    font-size: 0.2rem;
    line-height: 0.42rem;
    vertical-align: top;
    color: rgb(147, 153, 159);
  }

  .cart-add {
    display: inline-block;
    padding: 0.02rem;
    font-size: 0.36rem;
    line-height: 0.36rem;
    color: rgb(0, 160, 220);
  }
}
</style>
