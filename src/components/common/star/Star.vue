<template>
  <div class="stars">
    <span
      class="single-star"
      v-for="(starType,index) in starArray"
      :class="starType"
      :key="index"
      :style="{'width': imgSize, 'height':imgSize, 'margin-right':imgMargin,'margin-left':imgMargin}"
    ></span>
  </div>
</template>

<script>
export default {
  name: "Star",
  props: {
    size: Number,
    score: Number
  },
  computed: {
    imgSize() {
      return this.size + "rem";
    },
    imgMargin() {
      return this.size / 2.5 + "rem";
    },
    starArray() {
      let result = [];
      let score = Math.floor(this.score * 2) / 2;
      let hasDecimal = score % 1 !== 0;
      let integer = Math.floor(score);
      for (let i = 0; i < integer; i++) {
        result.push("on");
      }
      if (hasDecimal) {
        result.push("half");
      }
      while (result.length < 5) {
        result.push("off");
      }
      return result;
    }
  }
};
</script>

<style lang='stylus' scoped>
.stars {
  .single-star {
    display: inline-block;
    background-size: 100%;

    &.on {
      background-image: url('~img/star24_on@2x.png');
    }

    &.half {
      background-image: url('~img/star24_half@2x.png');
    }

    &.off {
      background-image: url('~img/star24_off@2x.png');
    }
  }
}
</style>
