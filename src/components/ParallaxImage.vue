<template>
  <div
    :style="{
      height: `${compensatedHeight}px`,
    }"
    class="ParallaxImage"
  >
    <ParallaxElement
      :factor="factor"
      :style="{
        top: `-${compensatedHeight / (1 / factor)}px`,
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
  inject: [`parallaxContainer`],
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
    compensatedHeight() {
      return this.innerHeight - (this.innerHeight * this.factor * 0.75);
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
    }
  },
};
</script>

<style lang="scss">
.ParallaxImage__aspect-ratio-wrap {
  height: 0;
  overflow: hidden;
  position: relative;
}

.ParallaxImage__aspect-ratio-inside {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}
</style>
