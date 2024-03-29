<template>
  <div id="app">
    <!-- <TheHeader /> -->

    <nav class="params">
      <ParamInput
        v-for="(param, index) in scaleParams"
        :key="index"
        :name="param.name"
        :label="param.label"
        :defaultValue="param.value"
        :info="param.info"
        @update:value="param.value = parseInt($event)"
      />
    </nav>

    <UnitsControl
      :rem="rem"
      :unit="unit"
      @update:unit="unit = $event"
      @update:rem="rem = $event"
    />

    <main class="steps">
      <Error
        v-if="isEmpty"
        errTitle="Couldn't generate scale"
        errMessage="Please make sure you fill in all parameters of the scale"
      />
      <ScaleStep
        v-else
        v-for="(step, index) in generated.slice().reverse()"
        :key="index"
        :step="step"
        :baseFontSize="generated[0].fontSize"
        :baseLineHeight="generated[0].lineHeight"
        :stepNumber="generated.length - index"
      />
    </main>

    <About />

    <!-- <a
      class="ph-badge"
      href="https://www.producthunt.com/posts/typeculator?utm_source=badge-top-post-badge&utm_medium=badge&utm_souce=badge-typeculator"
      target="_blank"
      rel="noreferrer"
    ><img
        src="https://api.producthunt.com/widgets/embed-image/v1/top-post-badge.svg?post_id=221736&theme=light&period=daily"
        alt="Typeculator - A different approach to generating type scales | Product Hunt Embed"
        style="width: 250px; height: 54px;"
        width="250px"
        height="54px"
      /></a> -->

    <a
      class="ph-badge"
      href="https://www.producthunt.com/posts/typeculator?utm_source=badge-featured&utm_medium=badge&utm_souce=badge-typeculator"
      target="_blank"
      rel="noreferrer"
    ><img
        src="https://api.producthunt.com/widgets/embed-image/v1/featured.svg?post_id=221736&theme=light"
        alt="Typeculator - A different approach to generating type scales | Product Hunt Embed"
        style="width: 250px; height: 54px;"
        width="250px"
        height="54px"
      /></a>
  </div>
</template>

<script>
// import TheHeader from './components/TheHeader.vue'
import ParamInput from './components/ParamInput.vue'
import ScaleStep from './components/ScaleStep.vue'
import UnitsControl from './components/UnitsControl.vue'
import Error from './components/Error.vue'
import About from './components/About.vue'

export default {
  name: 'App',
  components: {
    ParamInput,
    ScaleStep,
    UnitsControl,
    Error,
    About,
  },
  data() {
    return {
      scaleParams: {
        base: {
          name: 'base',
          label: 'Base size',
          info:
            'This is the base value from which the scale will be calculated. A value between 12 — 16 could be a good starting point for a type scale for screen design.',
          value: 16,
        },
        scaling: {
          name: 'scaling',
          label: 'Scaling factor',
          info:
            'This number controls the growth of your scale. A greater number will result in a bigger jump between the steps of your scale.',
          value: 3,
        },
        steps: {
          name: 'steps',
          label: 'Scale steps',
          info:
            'This is the number of steps your scale will have. For screen design, you could start with 4 — 6 steps and adjust as needed.',
          value: 6,
        },
        lhOffset: {
          name: 'lhOffset',
          label: 'Line height offset',
          info:
            'This is the value that controls your scale line-height. A greater number will result in a taller line-height for each of your scale steps.',
          value: 1,
        },
      },
      rem: 16,
      unit: 'px',
      generated: [],
    }
  },
  methods: {
    generateScale() {
      this.generated = []
      let prevSize = this.scaleParams.base.value
      for (let index = 0; index < this.scaleParams.steps.value; index++) {
        let size = prevSize + this.scaleParams.scaling.value * index
        let lineHeight =
          size +
          this.scaleParams.scaling.value *
            (index + this.scaleParams.lhOffset.value)

        let step = {
          fontSize:
            this.unit === 'px' ? size + this.unit : size / 16 + this.unit,
          lineHeight:
            this.unit === 'px'
              ? lineHeight + this.unit
              : lineHeight / 16 + this.unit,
          remAdjustedFontSize:
            this.unit === 'px' ? size + this.unit : size / this.rem + this.unit,
          remAdjustedLineHeight:
            this.unit === 'px'
              ? lineHeight + this.unit
              : lineHeight / this.rem + this.unit,
        }

        this.generated.push(step)

        prevSize = size
      }
    },
  },
  watch: {
    scaleParams: {
      deep: true,
      handler() {
        this.generateScale()
      },
    },
    rem: {
      handler() {
        this.generateScale()
      },
    },
    unit: {
      handler() {
        this.generateScale()
      },
    },
  },
  computed: {
    isEmpty() {
      return (
        isNaN(this.scaleParams.base.value) ||
        isNaN(this.scaleParams.scaling.value) ||
        isNaN(this.scaleParams.steps.value) ||
        isNaN(this.scaleParams.lhOffset.value) ||
        this.rem <= 0
      )
    },
  },
  mounted() {
    this.generateScale()
  },
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Roboto&family=Roboto+Mono&family=Roboto+Slab:wght@700&display=swap');

*,
*::before,
*::after {
  margin: 0;
  box-sizing: border-box;
}

:root {
  // Fonts
  --ui-font: 'Roboto';
  --sample-sans-font: 'Roboto';
  --sample-serif-font: 'Roboto Slab';
  --code-font: 'Roboto Mono';
  // Colors
  --primary-color: 255, 255, 255;
  --contrast-color: 24, 41, 82;
  --accent-color: 44, 54, 150;
  // Sizes
  --sidebar-width: 302px;
  --spacing: 32px;
  --spacing-md: 24px;
  --spacing-s: 16px;
  --spacing-xs: 8px;
  // Effects
  --box-shadow: 0px 16px 32px rgba(var(--contrast-color), 0.1);
  --rounding: 4px;
}

body::-webkit-scrollbar {
  width: 16px;
}
body {
  scrollbar-width: thin;
  scrollbar-color: rgba(var(--accent-color), 1);
}
body::-webkit-scrollbar-track {
  background: rgba(var(--contrast-color), 0.05);
}
body::-webkit-scrollbar-thumb {
  border-radius: 16px;
  background-color: rgba(var(--accent-color), 1);
  border: 4px solid rgba(var(--primary-color), 1);
}

#app {
  font-family: var(--ui-font), Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: rgba(var(--contrast-color), 1);
  min-height: 100vh;
  background-color: rgba(var(--contrast-color), 0.05);
}

.params {
  z-index: 1000;
  position: fixed;
  top: 0;
  left: 0;
  width: var(--sidebar-width);
  height: 100vh;
  background-color: rgba(var(--accent-color), 1);
  color: rgba(var(--primary-color), 1);
  padding: 0 0 var(--spacing) 0;
  overflow-y: auto;

  @media screen and (max-width: 900px) {
    position: static;
    height: auto;
    padding: var(--spacing-s) 0;
    width: 100%;
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    scrollbar-width: thin;
    scrollbar-color: rgba(var(--primary-color), 0.3);
  }

  &::-webkit-scrollbar {
    width: 16px;
  }
  &::-webkit-scrollbar-track {
    // background: rgba(var(--contrast-color), 0);
  }
  &::-webkit-scrollbar-thumb {
    border-radius: 16px;
    background-color: rgba(var(--primary-color), 0.3);
    border: 4px solid rgba(var(--accent-color), 1);
  }
}

.units {
  margin-left: var(--sidebar-width);
  padding: var(--spacing);
  padding-bottom: 0;

  @media screen and (max-width: 900px) {
    margin: 0;
    padding: var(--spacing-xs);
    padding-bottom: 0;
  }
}

.steps {
  margin-left: var(--sidebar-width);
  padding: var(--spacing);

  @media screen and (max-width: 900px) {
    margin-left: 0;
    padding: var(--spacing-xs);
  }
}

.about {
  margin-left: var(--sidebar-width);
  padding: var(--spacing);
  padding-top: 0;

  @media screen and (max-width: 900px) {
    margin: 0;
    padding: var(--spacing-xs);
    padding-top: 0;
  }
}

.ph-badge {
  display: inline-block;
  z-index: 1000;
  position: fixed;
  top: var(--spacing-s);
  right: var(--spacing-s);
  line-height: 0;

  @media screen and (max-width: 900px) {
    display: block;
    text-align: center;
    position: static;
    padding: var(--spacing);
    padding-top: 0;
  }
}

pre,
code {
  font-family: var(--code-font), monospace;
}

input,
button {
  font-family: inherit;
  font-size: inherit;
}

button:disabled {
  opacity: 0.2;
}
</style>
