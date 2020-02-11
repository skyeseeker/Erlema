<template>
  <div class="menu-wrapper">
    <ul class="menu">
      <li class="item-wrapper border-bottom" v-for="(item,index) in goodsData" :key="index">
        <div class="item-content">
          <span v-show="item.type>-1" class="item-icon" :class="classMap[item.type]"></span>
          <span class="item-text">{{item.name}}</span>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "GoodsMenu",
  data() {
    return {
      classMap: ["decrease", "discount", "special", "invoice", "guarantee"]
    };
  },
  props: {
    goodsData: Array
  },

  components: {}
};
</script>

<style lang='stylus' scoped>
@import '~style/mystyle.styl';

.border-bottom::before {
  border-bottom-color: rgba(7, 17, 27, 0.4);
  width: 80%;
  margin-left: 10%;
}

.menu-wrapper {
  flex: 0 0 22%;
  width: 22%;
  background: #f3f5f7;

  .menu {
    .item-wrapper {
      display: table;
      width: 100%;
      height: 1.1rem;

      .item-content {
        display: table-cell;
        vertical-align: middle;
        padding-left 10%
        padding-right 5%
        font-size 0

        .item-text {
          font-size: 0.26rem;
          font-weight: 200;
          color: rgb(24, 20, 20);
        }

        .item-icon {
          display: inline-block;
          vertical-align: top;
          width: 0.3rem;
          height: 0.3rem;
          background-size: 100%;
          background-repeat: no-repeat;
          addDiscountClass();
        }
      }
    }
  }
}
</style>
