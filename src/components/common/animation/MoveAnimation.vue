<template>
  <transition>
    <slot></slot>
  </transition>
</template>

<script>
export default {
  name: "MoveAnimation"
};
</script>

<style lang="stylus" scoped>
.v-enter, .v-leave-to {
  transform: translate3d(10px,0,0)
  opacity: 0;
}

.v-enter-active, .v-leave-active {
  transition: all .3s linear
}
</style>