<template>
  <div class="units">
    <div class="units-control">
      <button
        class="units-toggle"
        @click="togglePxRem()"
      >
        <span
          class="units-toggle__value"
          :class="{'active': currentUnit === 'px'}"
        >Px</span>
        <span
          class="units-toggle__value"
          :class="{'active': currentUnit === 'rem'}"
        >Rem</span>
      </button>
      <span
        class="units-control__rem"
        v-if="currentUnit==='rem'"
      >1 rem = <strong>{{ currentRem }}</strong> px</span>
      <div
        class="units-control__rem-value"
        v-if=" currentUnit==='rem'"
      >
        <button
          :disabled="currentRem <= 0 ? true : false"
          class="units-control__spinner"
          @click="currentRem--"
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
              fill="rgb(var(--accent-color))"
            />
          </svg>
        </button>
        <input
          class="units-control__input"
          type="number"
          min="1"
          max="999999999"
          step="1"
          v-model.number="currentRem"
        >
        <button
          class="units-control__spinner"
          @click="currentRem++"
        ><svg
            width="8"
            height="8"
            viewBox="0 0 8 8"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              d="M3 7C3 7.55228 3.44769 8 4 8C4.55231 8 5 7.55228 5 7V5H7C7.55231 5 8 4.55228 8 4C8 3.44772 7.55231 3 7 3H5V1C5 0.447723 4.55231 0 4 0C3.44769 0 3 0.447723 3 1V3H1C0.447693 3 0 3.44772 0 4C0 4.55228 0.447693 5 1 5H3V7Z"
              fill="rgb(var(--accent-color))"
            />
          </svg>
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'UnitControl',
  props: {
    unit: {
      type: String,
      required: true
    },
    rem: {
      type: Number,
      required: true
    }
  },
  data() {
    return {
      currentUnit: this.unit,
      currentRem: parseInt(this.rem)
    }
  },
  methods: {
    togglePxRem() {
      this.currentUnit === 'px'
        ? (this.currentUnit = 'rem')
        : (this.currentUnit = 'px')
    }
  },
  watch: {
    currentUnit: {
      handler(value) {
        this.$emit('update:unit', value)
      }
    },
    currentRem: {
      handler(value) {
        this.$emit('update:rem', value)
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.units-control {
  display: flex;
  align-items: center;
  overflow: hidden;
  border-radius: var(--rounding);
  background-color: rgba(var(--primary-color), 1);
  box-shadow: var(--box-shadow);
  padding: var(--spacing-s);

  @media screen and (max-width: 900px) {
    display: block;
    text-align: center;
  }

  &__rem {
    min-width: 120px;
    text-align: right;
    margin: 0 var(--spacing-s);
    text-transform: uppercase;

    @media screen and (max-width: 900px) {
      display: block;
      margin: var(--spacing-s) 0;
      text-align: center;
    }
  }

  &__rem-value {
    display: flex;
    justify-content: center;
    align-items: center;
  }

  &__input {
    width: 80px;
    height: 40px;
    margin: 0 var(--spacing-s);
    background-color: rgba(var(--accent-color), 0);
    border: 1px solid rgba(var(--accent-color), 0.6);
    border-radius: var(--rounding);
    color: rgba(var(--accent-color), 1);
    text-align: center;
    -moz-appearance: textfield;

    &::-webkit-outer-spin-button,
    &::-webkit-inner-spin-button {
      -webkit-appearance: none;
    }

    @media screen and (max-width: 900px) {
      width: 100%;
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
    background-color: rgba(var(--accent-color), 0);
    border: 1px solid rgba(var(--accent-color), 0.6);
    border-radius: var(--rounding);
  }

  &__input,
  &__spinner {
    &:focus,
    &:hover {
      outline: none;
      box-shadow: 0 0 0 2px rgba(var(--accent-color), 0.4);
      border-color: rgba(var(--accent-color), 1);
    }
  }
}

.units-toggle {
  padding: 0;
  border: none;
  outline: none;
  border-radius: var(--rounding);
  background-color: rgba(var(--accent-color), 0.1);

  @media screen and (max-width: 900px) {
    display: flex;
    width: 100%;
  }

  &__value {
    height: 40px;
    display: inline-flex;
    align-items: center;
    justify-content: center;
    padding: var(--spacing-xs) var(--spacing-s);
    border-radius: var(--rounding);
    margin: 0;

    @media screen and (max-width: 900px) {
      flex: 1;
    }

    &.active {
      background-color: rgba(var(--accent-color), 1);
      color: rgba(var(--primary-color), 1);
    }
  }
}
</style>