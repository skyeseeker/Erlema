<template>
  <div class="goods">
    <goods-menu :goodsData="goodsData" :currentIndex="currentIndex" @clickMenu="changeFoods"></goods-menu>
    <foods :goodsData="goodsData" @myIndex="showIndex" :selectedIndex="selectedIndex"></foods>
    <!-- <shop-car></shop-car> -->
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
      selectedIndex:0
    };
  },
  methods: {
    changeFoods(index){
      this.selectedIndex=index
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
        console.log(this.goodsData);
      }
    }
  },
  created() {
    this.getGoodsData();
  },
  components: {
    GoodsMenu,
    Foods
    // ShopCar
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
}
</style>
