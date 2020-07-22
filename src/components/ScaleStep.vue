<template>
  <div class="step">
    <div class="step__sample">
      <p :style="`font-size: ${step.fontSize}; line-height: ${step.lineHeight};`">The quick brown fox jumps over a lazy dog</p>
    </div>
    <div class="step__body">
      <p :style="`font-size: ${baseFontSize}; line-height: ${baseLineHeight};`">
        Lorem ipsum dolor sit amet consectetur, adipisicing elit. Fugiat ratione eum officiis delectus recusandae exercitationem? Sunt vitae fuga voluptatibus iste sed assumenda necessitatibus! Cum dignissimos repellendus dicta ipsam quaerat tempore.
      </p>
    </div>
    <div class="step__css">
      <pre><code><span class="selector">.scale-step-{{ stepNumber }}</span> { <br class="mobile-only"><span class="rule">font-size: <span class="value">{{ step.remAdjustedFontSize }}</span></span>; <br class="mobile-only"><span class="rule">line-height: <span class="value">{{ step.remAdjustedLineHeight }}</span></span>; <br class="mobile-only">}</code></pre>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ScaleStep',
  props: {
    step: {
      type: Object,
      required: true
    },
    baseFontSize: {
      type: String,
      required: true
    },
    baseLineHeight: {
      type: String,
      required: true
    },
    stepNumber: {
      type: Number,
      required: true
    }
  }
}
</script>

<style lang="scss">
.step {
  background-color: rgba(var(--primary-color), 1);
  padding: var(--spacing);
  border-radius: var(--rounding);
  box-shadow: var(--box-shadow);

  @media screen and (max-width: 900px) {
    padding: var(--spacing-s) var(--spacing-md);
  }

  &:not(:last-child) {
    margin-bottom: var(--spacing-xs);
  }

  &__sample {
    letter-spacing: -0.05em;
    font-family: var(--sample-serif-font), sans-serif;
    color: rgba(var(--contrast-color), 1);
  }

  &__body {
    font-family: var(--sample-sans-font), serif;
    color: rgba(var(--contrast-color), 0.8);
    margin: var(--spacing-s) 0 var(--spacing) 0;
  }

  &__css {
    overflow-x: auto;
    position: relative;
    background-color: rgba(var(--contrast-color), 0.05);
    padding: var(--spacing-s) var(--spacing-md);
    border-radius: var(--rounding);

    .selector {
      color: #ae1c00;
    }
    .rule {
      color: #ae0060;

      @media screen and (max-width: 600px) {
        margin-left: 20px;
      }
    }
    .value {
      color: rgba(var(--accent-color), 1);
    }

    .mobile-only {
      display: none;

      @media screen and (max-width: 600px) {
        display: block;
      }
    }
  }
}
</style>