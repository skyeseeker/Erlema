<template>
  <div>
    <ul>
      <li v-for="(item, index) in goodsData" :key='index'>
        <div>{{item.name}}</div>
        <ul>
          <li v-for="(food,index) in item.foods" :key='index'>
            {{food.name}}
          </li>
        </ul>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'Foods',
  data () {
    return {
    }
  },
  props:{
    goodsData:Array
  },
}
</script>

<style lang='stylus' scoped>
</style>
