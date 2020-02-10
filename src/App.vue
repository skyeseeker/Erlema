<template>
  <div id="app">
    <my-header :seller='sellerData'></my-header>

    <div class="navigBar border-bottom">
      <router-link to="/goods" type="div" class="navigBar-content">商品</router-link>

      <router-link to="/ratings" type="div" class="navigBar-content">评价</router-link>

      <router-link to="/seller" type="div" class="navigBar-content">商家</router-link>
    </div>

    <div class="content">
      <router-view />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import MyHeader from "./components/header/Header";
export default {
  name: "App",
  components: {
    MyHeader
  },
  data() {
    return {
      sellerData: {}
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
        this.sellerData = data.data;
        console.log(this.sellerData);
      }
    }
  },
  created() {
    this.getSellerData();
  }
};
</script>

<style lang="stylus" scoped>
.navigBar {
  display: flex;
  width: 100%;
  height: 0;
  padding-bottom: 12%;

  .navigBar-content {
    flex: 1;
    text-align: center;
    height: 0.864rem;
    line-height: 0.864rem;
    font-size: 0.36rem;
    color: rgb(77, 85, 93);
  }
}
</style>
