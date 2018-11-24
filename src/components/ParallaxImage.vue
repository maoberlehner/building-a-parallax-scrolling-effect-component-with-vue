<template>
  <ParallaxElement
    :factor="factor"
    class="ParallaxImage"
    :style="{
      position: `relative`,
      top: `-${factor * 100}%`,
    }"
  >
    <slot/>
  </ParallaxElement>
</template>

<script>
import ParallaxElement from './ParallaxElement.vue';

export default {
  name: `ParallaxImage`,
  components: {
    ParallaxElement,
  },
  props: {
    factor: {
      default: 0.25,
      type: Number,
    },
  },
};
</script>
