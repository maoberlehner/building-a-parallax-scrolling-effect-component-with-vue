<template>
  <div
    class="ParallaxContainer"
    @load.capture="calcParallax"
  >
    <slot/>
  </div>
</template>

<script>
export default {
  name: `ParallaxContainer`,
  provide() {
    return {
      parallaxContainer: this.data,
    };
  },
  data() {
    return {
      data: {
        height: 0,
        scrollFactor: 0,
        width: 0,
      },
    };
  },
  computed: {
    elements() {
      return this.$slots.default.map(({ child }) => child);
    },
  },
  mounted() {
    this.calcParallax();

    // We're using a `requestAnimationFrame()`
    // for optimal performance.
    const eventHandler = () => requestAnimationFrame(this.calcParallax);
    window.addEventListener(`resize`, eventHandler);
    window.addEventListener(`scroll`, eventHandler);
    // Remove the scroll hanlder when the
    // component is destroyed.
    this.$on(`hook:destroyed`, () => {
      window.removeEventListener(`resize`, eventHandler);
      window.removeEventListener(`scroll`, eventHandler);
    });
  },
  methods: {
    calcParallax() {
      const containerRect = this.$el.getBoundingClientRect();

      this.data.height = containerRect.height;
      this.data.width = containerRect.width;

      const containerViewportOffsetTop = containerRect.top;
      this.data.scrollFactor = (containerViewportOffsetTop + this.data.height) / (window.innerHeight + this.data.height);
    },
  },
};
</script>

<style lang="scss">
.ParallaxContainer {
  overflow: hidden;
  position: relative;
}
</style>
