<template>
  <div class="param">
    <label
      class="param__label"
      :for="name"
    >{{ label }}</label>
    <div class="param__control">
      <button
        :disabled="value <= 0 ? true : false"
        class="param__spinner"
        :aria-label="`Decrease ${label.toLowerCase()} by one`"
        @click="value--"
      ><svg
          width="8"
          height="2"
          viewBox="0 0 8 2"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <rect
            width="8"
            height="2"
            rx="1"
            fill="rgb(var(--primary-color))"
          />
        </svg>
      </button>
      <input
        class="param__input"
        type="number"
        min="1"
        max="999999999"
        step="1"
        v-model.number="value"
        :name="name"
        :id="name"
      >
      <button
        class="param__spinner"
        @click="value++"
        :aria-label="`Increase ${label.toLowerCase()} by one`"
      ><svg
          width="8"
          height="8"
          viewBox="0 0 8 8"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            d="M3 7C3 7.55228 3.44769 8 4 8C4.55231 8 5 7.55228 5 7V5H7C7.55231 5 8 4.55228 8 4C8 3.44772 7.55231 3 7 3H5V1C5 0.447723 4.55231 0 4 0C3.44769 0 3 0.447723 3 1V3H1C0.447693 3 0 3.44772 0 4C0 4.55228 0.447693 5 1 5H3V7Z"
            fill="rgb(var(--primary-color))"
          />
        </svg>
      </button>
    </div>
    <p class="param__info">{{ info }}</p>
  </div>
</template>

<script>
export default {
  name: 'ParamInput',
  props: {
    name: String,
    label: String,
    info: String,
    defaultValue: Number
  },
  data() {
    return {
      value: this.defaultValue
    }
  },
  watch: {
    value: {
      handler(value) {
        this.$emit('update:value', value)
      }
    }
  }
}
</script>

<style scoped lang="scss">
.param {
  padding: 0 var(--spacing);
  margin: var(--spacing) 0;

  @media screen and (max-width: 900px) {
    padding: 0 var(--spacing-md);
    margin: var(--spacing-xs) 0;
  }

  &:last-of-type {
    border-bottom: 0;
  }

  &__label {
    font-size: 12px;
    line-height: 16px;
    letter-spacing: 0.1em;
    text-transform: uppercase;
  }

  &__control {
    margin: var(--spacing-s) 0;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  &__input {
    min-width: 0;
    height: 40px;
    margin: 0 var(--spacing-s);
    background-color: rgba(var(--primary-color), 0);
    border: 1px solid rgba(var(--primary-color), 0.6);
    border-radius: var(--rounding);
    color: rgba(var(--primary-color), 1);
    text-align: center;
    -moz-appearance: textfield;

    &::-webkit-outer-spin-button,
    &::-webkit-inner-spin-button {
      -webkit-appearance: none;
    }
  }

  &__spinner {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-shrink: 0;
    width: 40px;
    height: 40px;
    margin: 0;
    padding: 0;
    background-color: rgba(var(--primary-color), 0);
    border: 1px solid rgba(var(--primary-color), 0.6);
    border-radius: var(--rounding);
  }

  &__input,
  &__spinner {
    &:focus,
    &:hover {
      outline: none;
      box-shadow: 0 0 0 2px rgba(var(--primary-color), 0.4);
      border-color: rgba(var(--primary-color), 1);
    }
  }

  &__info {
    font-size: 12px;
    line-height: 16px;
    font-weight: 400;
    letter-spacing: 0.02em;
    color: rgba(var(--primary-color), 0.8);
  }
}
</style>