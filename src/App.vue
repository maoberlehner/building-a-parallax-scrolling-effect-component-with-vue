<template>
  <div class="App o-container o-container--s o-vertical-spacing o-vertical-spacing--xl">
    <h1>Building a Parallax Scrolling Effect Component with Vue.js</h1>

    <section class="App__example o-vertical-spacing o-vertical-spacing--l">
      <h2>Single element</h2>

      <ParallaxContainer class="App__example-single-element">
        <ParallaxElement
          :factor="0.25"
          class="App__example-element"
        >
          <h2>Lorem Ipsum</h2>
          <p>Lorem ipsum dolor sit amet, consetetur sadipscing elitr.</p>
        </ParallaxElement>
      </ParallaxContainer>
    </section>

    <section class="App__example o-vertical-spacing o-vertical-spacing--l">
      <h2>Multiple elements</h2>

      <ParallaxContainer class="App__example-double-element">
        <ParallaxElement
          :factor="0.25"
          class="App__example-element"
        >
          <h2>Lorem Ipsum</h2>
          <p>Lorem ipsum dolor sit amet, consetetur sadipscing elitr.</p>
        </ParallaxElement>
        <ParallaxElement
          :factor="0.5"
          class="App__example-element"
        >
          <h2>Sadipscing Ipsum</h2>
          <p>Sadipscing ipsum dolor sit amet, consetetur lorem elitr.</p>
        </ParallaxElement>
      </ParallaxContainer>
    </section>

    <section class="App__example o-vertical-spacing o-vertical-spacing--l">
      <h2>Image element</h2>

      <ParallaxContainer
        :style="{
          height: `160px`
        }"
      >
        <ParallaxImage :factor="0.5">
          <img
            src="https://images.unsplash.com/photo-1516750930166-ed88ab1adb61?ixlib=rb-0.3.5&ixid=eyJhcHBfaWQiOjEyMDd9&s=65c8f6fcafaf68f5fa434b5f076780fd&auto=format&fit=crop&h=300&q=80"
            alt="Road that leads to a mountain"
          >
        </ParallaxImage>
      </ParallaxContainer>
    </section>

    <section class="App__example o-vertical-spacing o-vertical-spacing--l">
      <h2>Just for scrolling</h2>

      <p>
        Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam
        nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat,
        sed diam voluptua. At vero eos et accusam et justo duo dolores et ea
        rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem
        ipsum dolor sit amet. Lorem ipsum dolor sit amet, consetetur sadipscing
        elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna
        aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo
        dolores et ea rebum. Stet clita kasd gubergren, no sea takimata sanctus
        est Lorem ipsum dolor sit amet.
      </p>
      <p>
        Sed diam voluptua. At vero eos et accusam et justo duo dolores et ea
        rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem
        ipsum dolor sit amet. Lorem ipsum dolor sit amet, consetetur sadipscing
        elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna
        aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo
        dolores et ea rebum. Stet clita kasd gubergren, no sea takimata sanctus
        est Lorem ipsum dolor sit amet.
      </p>
      <p>
        Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam
        nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat,
        sed diam voluptua. At vero eos et accusam et justo duo dolores et ea
        rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem
        ipsum dolor sit amet. Lorem ipsum dolor sit amet, consetetur sadipscing
        elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna
        aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo
        dolores et ea rebum. Stet clita kasd gubergren, no sea takimata sanctus
        est Lorem ipsum dolor sit amet.
      </p>
      <p>
        Sed diam voluptua. At vero eos et accusam et justo duo dolores et ea
        rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem
        ipsum dolor sit amet. Lorem ipsum dolor sit amet, consetetur sadipscing
        elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna
        aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo
        dolores et ea rebum. Stet clita kasd gubergren, no sea takimata sanctus
        est Lorem ipsum dolor sit amet.
      </p>
      <p>
        Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam
        nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat,
        sed diam voluptua. At vero eos et accusam et justo duo dolores et ea
        rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem
        ipsum dolor sit amet. Lorem ipsum dolor sit amet, consetetur sadipscing
        elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna
        aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo
        dolores et ea rebum. Stet clita kasd gubergren, no sea takimata sanctus
        est Lorem ipsum dolor sit amet.
      </p>
      <p>
        Sed diam voluptua. At vero eos et accusam et justo duo dolores et ea
        rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem
        ipsum dolor sit amet. Lorem ipsum dolor sit amet, consetetur sadipscing
        elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna
        aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo
        dolores et ea rebum. Stet clita kasd gubergren, no sea takimata sanctus
        est Lorem ipsum dolor sit amet.
      </p>
    </section>
  </div>
</template>

<script>
import ParallaxContainer from './components/ParallaxContainer.vue';
import ParallaxElement from './components/ParallaxElement.vue';
import ParallaxImage from './components/ParallaxImage.vue';

export default {
  name: `App`,
  components: {
    ParallaxContainer,
    ParallaxElement,
    ParallaxImage,
  },
};
</script>

<style lang="scss">
@import './assets/scss/settings/**/*';
@import './assets/scss/generic/**/*';
@import '{
  .o-container,
  .o-container--s,
} from ~@avalanche/object-container';
@import '{
  .o-vertical-spacing,
  .o-vertical-spacing--l,
  .o-vertical-spacing--xl,
} from ~@avalanche/object-vertical-spacing';

.App {
  padding-top: setting-spacing(xl);
  padding-bottom: setting-spacing(xl);

  h1 {
    text-align: center;
  }
}

.App__example {
  padding: setting-spacing(l);
  border-radius: 0.25em;
  box-shadow: 0 0.35em 1em rgba(#000, 0.2);
}

.App__example-single-element {
  height: 20em;
  background-color: lightblue;
}

.App__example-double-element {
  display: flex;
  height: 20em;
  background-color: lightgreen;
}

.App__example-element {
  padding: 1em;
  max-width: 12em;

  &:nth-child(2) {
    top: 2em;
  }
}
</style>
