<template>
  <div
    class="ParallaxElement"
    :style="{
      transform: `translate3d(0, ${offset}px, 0)`,
    }"
  >
    <slot/>
  </div>
</template>

<script>
export default {
  name: `ParallaxElement`,
  inject: [`parallaxContainer`],
  props: {
    factor: {
      default: 0.25,
      type: Number,
    },
  },
  computed: {
    offset() {
      const { height, scrollFactor } = this.parallaxContainer;
      return scrollFactor * height * this.factor;
    },
  },
};
</script>
