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
    aspectRatio: {
      default: 9 / 16,
      type: Number,
    },
    factor: {
      default: 0.25,
      type: Number,
    },
  },
  data() {
    return {
      height: 0,
    };
  },
  computed: {
    compensatedHeight() {
      return this.height - (this.height * this.factor * 0.75);
    },
  },
  mounted() {
    this.setHeight();

    const eventHandler = () => requestAnimationFrame(this.setHeight);
    window.addEventListener(`resize`, eventHandler);
    this.$on(`hook:destroyed`, () => {
      window.removeEventListener(`resize`, eventHandler);
    });
  },
  methods: {
    setHeight() {
      this.height = this.$refs.inside.getBoundingClientRect().height;
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
