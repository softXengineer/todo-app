<template>
  <h1 class="section-header">
    <span class="section-header__icon">{{ icon }}</span>
    {{ title }}
  </h1>
</template>

<script>
export default {
  name: "SectionHeader",
  props: {
    icon: String,
    title: String,
  },
};
</script>

<style lang="scss">
.section-header {
  color: #37352f;

  &__icon {
    font-size: 2rem;
    margin-right: 6px;
  }
}

@media (min-width: 0px) and (max-width: 576px) {
  .section-header {
    font-size: 1.2rem;
    &__icon {
      font-size: 1.3rem;
      margin-right: 0.6rem;
    }
  }
}

@media (min-width: 576px) and (max-width: 1200px) {
  .section-header {
    font-size: 1.5rem;
    &__icon {
      font-size: 1.6rem;
      margin-right: 0.6rem;
    }
  }
}
</style>
