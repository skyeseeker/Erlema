<template>
  <div id="app">
    <my-header></my-header>

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
import MyHeader from "./components/header/Header";
export default {
  name: "App",
  components: {
    MyHeader
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
