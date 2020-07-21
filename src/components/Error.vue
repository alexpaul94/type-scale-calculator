<template>
  <div class="error">
    <img
      class="error__img"
      src="../assets/error.svg"
      :alt="errMessage"
    >
    <p class="error__title">{{ errTitle }}</p>
    <p class="error__msg">{{ errMessage }}</p>
  </div>
</template>

<script>
export default {
  name: 'Error',
  props: {
    errTitle: String,
    errMessage: String
  }
}
</script>

<style lang="scss">
.error {
  text-align: center;
  background-color: rgba(var(--primary-color), 1);
  padding: var(--spacing);
  border-radius: var(--rounding);
  box-shadow: var(--box-shadow);

  &__img,
  &__title,
  &__msg {
    margin: var(--spacing-xs) auto;
  }

  &__img {
    max-width: 10vw;
  }

  &__title {
    font-size: 24px;
    color: rgba(var(--accent-color), 1);
  }

  &__msg {
    color: rgba(var(--contrast-color), 0.8);
  }
}
</style>