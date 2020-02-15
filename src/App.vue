<template>
  <div id="app">
    <my-header :seller="seller"></my-header>

    <div class="navigBar border-bottom">
      <router-link to="/goods" class="navigBar-content">商品</router-link>
      <router-link to="/ratings" class="navigBar-content">评价</router-link>
      <router-link to="/seller" class="navigBar-content">商家</router-link>
    </div>

    <div class="content">
      <keep-alive>
        <router-view></router-view>
      </keep-alive>
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
      seller: {}
    };
  },
  created() {
    this.getSellerData();
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
    }
  }
};
</script>

<style lang="stylus" scoped>
.navigBar {
  display: flex;
  width: 100%;

  .navigBar-content {
    flex: 1;
    text-align: center;
    height: 0.86rem;
    line-height: 0.86rem;
    font-size: 0.36rem;
    color: rgb(77, 85, 93);
  }
}
</style>
