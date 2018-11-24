<template>
  <div class="ParallaxElement">
    <slot/>
  </div>
</template>

<script>
export default {
  name: `ParallaxElement`,
  props: {
    factor: {
      default: 0.25,
      type: Number,
    },
  },
};
</script>
