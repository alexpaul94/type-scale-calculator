<template>
  <aside class="about">
    <div class="about__content">
      <img
        class="about__logo"
        src="../assets/logo.svg"
        alt="Typeculator - typescale generator"
      >
      <p class="about__body">
        Typeculator is a simple type scale calculator based on the "Golden Thread" technique. I got inspired to build this after reading <a
          href="https://medium.com/design-ibm/a-deep-dive-on-typescales-16c7b1473d83"
          title="Medium article about typescales"
          rel="noreferrer"
          target="_blank"
        >this article</a> where the technique is explained.
      </p>

      <p class="about__links">
        <a
          href="https://github.com/alexpaul94/type-scale-calculator"
          title="Typeculator Github page"
          rel="noreferrer"
          target="_blank"
        >Github</a>
        <a
          href="https://dribbble.com/AlexPaul"
          title="Alex Paul's Dribbble profile"
          rel="noreferrer"
          target="_blank"
        >Dribbble</a>
        <a
          href="https://www.instagram.com/alexpaul.me/"
          title="Alex Paul's Instagram profile"
          rel="noreferrer"
          target="_blank"
        >Instagram</a>
        <a
          href="https://twitter.com/alexpaul_design"
          title="Alex Paul's Twitter profile"
          rel="noreferrer"
          target="_blank"
        >Twitter</a>
        <a
          href="https://alexpaul.me"
          title="Alex Paul's website"
          rel="noreferrer"
          target="_blank"
        >Website</a>
      </p>

    </div>
  </aside>
</template>

<script>
export default {
  name: 'About'
}
</script>

<style lang="scss">
.about {
  text-align: center;

  &__content {
    background-color: rgba(var(--primary-color), 1);
    padding: var(--spacing);
    border-radius: var(--rounding);
    box-shadow: var(--box-shadow);

    @media screen and (max-width: 900px) {
      padding: var(--spacing-s) var(--spacing-md);
    }
  }

  &__logo {
    max-width: 200px;
    margin-bottom: var(--spacing-s);
  }

  &__body {
    line-height: 1.6;
    color: rgba(var(--contrast-color), 0.8);

    a {
      color: rgba(var(--accent-color), 1);
    }
  }

  &__links {
    display: grid;
    justify-items: center;
    grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));
    grid-template-rows: auto;
    grid-gap: var(--spacing-s);
    margin-top: var(--spacing);
    padding-top: var(--spacing);
    border-top: 1px solid rgba(var(--contrast-color), 0.1);

    a {
      font-size: 14px;
      text-transform: uppercase;
      text-decoration: none;
      color: rgba(var(--accent-color), 1);
    }
  }
}
</style>