<template>
  <div>
    <div v-for="(item,index) in balls" :key="index">
      <transition @before-enter="beforeEnter" @enter="enter" @after-enter="afterEnter">
        <div class="ball" v-show="item.show">
          <div class="inner innerHook"></div>
        </div>
      </transition>
    </div>
  </div>
</template>

<script>
export default {
  name: "DropAnimation",
  data() {
    return {
      // isShow: false,
      balls: [
        { show: false },
        { show: false },
        { show: false },
        { show: false },
        { show: false }
      ],
      dropBalls: []
    };
  },
  props: {
    diffPos: Object
  },
  watch: {
    diffPos() {
      this.drop(this.diffPos);
    },
    dropBalls(){
      console.log(this.dropBalls.length)
    }
  },
  methods: {
    drop(pos) {
      for (let i = 0; i < this.balls.length; i++) {
        let ball = this.balls[i];
        if (!ball.show) {
          ball.show = true;
          ball.pos = pos;
          this.dropBalls.push(ball);
          return;
        }
      }
    },
    beforeEnter(el) {
      let count = this.balls.length;
      while (count--) {
        let ball = this.balls[count];
        if (ball.show) {
          el.style.opacity = 0;
          el.style.transform = `translate3d(${ball.pos.x}px,0,0)`;
          // let inner = this.$refs.innerHook[ball.index];
          // 列表循环，通过上面vue提供的 ref 和 this.$refs ，取得的是一个列表DOM数组
          // 而用js原生的 getElementsByClassName 可以只取得一个列表DOM
          let inner = el.getElementsByClassName("innerHook")[0];
          inner.style.transform = `translate3d(0,${ball.pos.y}px,0)`;
        }
      }
    },
    enter(el) {
      let rf = el.offsetHeight;
      this.$nextTick(() => {
        el.style.opacity = 1;
        el.style.transform = "translate3d(0,0,0)";
        el.style.transition = "all .6s linear";
        // let inner = this.$refs.innerHook[ball.index];
        let inner = el.getElementsByClassName("innerHook")[0];
        inner.style.transform = "translate3d(0,0,0)";
        inner.style.transition = "all .6s cubic-bezier(.39,-0.58,1,.58)";
      });
    },
    afterEnter(el) {
      el.style.opacity = 0;
      let ball = this.dropBalls.shift();
      if (ball) {
        ball.show = false;
      }
    }
  }
};
</script>

<style lang="stylus" scoped>
.ball {
  .inner {
    position: fixed;
    left: 0.6rem;
    bottom: 0.5rem;
    z-index: 10;
    width: 0.4rem;
    height: 0.4rem;
    border-radius: 50%;
    background-color: rgb(8, 169, 220);
  }
}
</style>