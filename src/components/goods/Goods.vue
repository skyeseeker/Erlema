<template>
  <div class="goods">
    <goods-menu :goodsData="goodsData" :currentIndex="currentIndex" @clickMenu="changeFoods"></goods-menu>
    <foods
      :goodsData="goodsData"
      @myIndex="showIndex"
      :selectedIndex="selectedIndex"
      @deliverAddDom="handleAddDom"
    ></foods>
    <shop-car :selectedFoods="selectedFoods" :buttonDom="buttonDom"></shop-car>
  </div>
</template>

<script>
import axios from "axios";
import GoodsMenu from "./menu/Menu";
import Foods from "./foods/Foods";
import ShopCar from "./shopCar/ShopCar";

export default {
  name: "Goods",
  data() {
    return {
      goodsData: [],
      currentIndex: 0,
      selectedIndex: 0,
      buttonDom: null
    };
  },
  computed: {
    selectedFoods() {
      let foods = [];
      this.goodsData.forEach(good => {
        good.foods.forEach(food => {
          if (food.count) {
            foods.push(food);
          }
        });
      });
      return foods;
    }
  },
  methods: {
    handleAddDom(buttonDom) {
      this.buttonDom = buttonDom;
    },
    changeFoods(index) {
      this.selectedIndex = index;
    },
    showIndex(index) {
      this.currentIndex = index;
    },
    getGoodsData() {
      axios
        .get("/api/goods")
        .then(this.getGoodsDataSucc)
        .catch(err => {
          console.log(err);
        });
    },
    getGoodsDataSucc(res) {
      const data = res.data;
      if (data.errno == 0 && data.data) {
        this.goodsData = data.data;
      }
    }
  },
  created() {
    this.getGoodsData();
  },
  components: {
    GoodsMenu,
    Foods,
    ShopCar
  }
};
</script>

<style lang='stylus' scoped>
.goods {
  display: flex;
  position: absolute;
  top: 3.56rem;
  bottom: 0;
  left: 0;
  right: 0;
  padding-bottom: 1rem;
}
</style>
