<template>
  <div
    :style="{
      height: `${compensatedHeight}px`,
    }"
    class="ParallaxImage"
  >
    <ParallaxElement
      :factor="compensatedFactor"
      :style="{
        paddingTop: `${aspectRatio * 100}%`,
      }"
      class="ParallaxImage__aspect-ratio-wrap"
    >
      <div
        ref="inside"
        class="ParallaxImage__aspect-ratio-inside"
      >
        <slot/>
      </div>
    </ParallaxElement>
  </div>
</template>

<script>
import ParallaxElement from './ParallaxElement.vue';

export default {
  name: `ParallaxImage`,
  components: {
    ParallaxElement,
  },
  props: {
    width: {
      required: true,
      type: Number,
    },
    height: {
      required: true,
      type: Number,
    },
    factor: {
      default: 0.25,
      type: Number,
    },
  },
  data() {
    return {
      innerHeight: 0,
    };
  },
  computed: {
    aspectRatio() {
      return this.height / this.width;
    },
    compensatedFactor() {
      // Because the parallax effect is relative
      // to the containers height and because we
      // shrink the containers height by the given
      // factor, we have to compensate this by
      // increasing the factor.
      return this.factor * 2;
    },
    compensatedHeight() {
      // We want the image to scroll inside of a
      // container to prevent the image scrolling
      // above its sourounding elements. The
      // container must be shrinked by the given
      // factor to make sure we don't have any
      // whitespace when scrolling.
      return this.innerHeight - (this.innerHeight * this.factor);
    },
  },
  mounted() {
    this.setInnerHeight();

    const eventHandler = () => requestAnimationFrame(this.setInnerHeight);
    window.addEventListener(`resize`, eventHandler);
    this.$on(`hook:destroyed`, () => {
      window.removeEventListener(`resize`, eventHandler);
    });
  },
  methods: {
    setInnerHeight() {
      this.innerHeight = this.$refs.inside.getBoundingClientRect().height;
    },
  },
};
</script>

<style lang="scss">
.ParallaxImage__aspect-ratio-wrap {
  position: relative;
  top: -100%;
  height: 0;
  overflow: hidden;
}

.ParallaxImage__aspect-ratio-inside {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}
</style>
