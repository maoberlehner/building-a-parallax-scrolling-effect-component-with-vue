<template>
  <div class="ParallaxContainer">
    <slot/>
  </div>
</template>

<script>
export default {
  name: `ParallaxContainer`,
  computed: {
    elements() {
      return this.$slots.default.map(({ child }) => child);
    },
  },
  mounted() {
    this.calcParallax();

    // We're using a `requestAnimationFrame()`
    // for optimal performance.
    const scrollHandler = () => requestAnimationFrame(this.calcParallax);
    window.addEventListener(`scroll`, scrollHandler);
    // Remove the scroll hanlder when the
    // component is destroyed.
    this.$on(`destroyed`, () => {
      window.removeEventListener(`scroll`, scrollHandler);
    });
  },
  methods: {
    calcParallax() {
      const containerRect = this.$el.getBoundingClientRect();
      const containerHeight = containerRect.height;
      const containerViewportOffsetTop = this.$el.getBoundingClientRect().top;
      // Position relative to the viewport.
      const viewportPosition = containerViewportOffsetTop / (window.innerHeight * 0.01);
      // Position relative to the container.
      const containerPosition = containerHeight * viewportPosition * 0.01;

      this.elements.forEach((component) => {
        component.$el.style.transform = `translate3d(0, ${containerPosition * component.factor}px, 0)`;
      });
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
