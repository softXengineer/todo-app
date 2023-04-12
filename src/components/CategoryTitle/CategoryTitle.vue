<template>
  <div class="category__title">
    <SectionHeader :icon="icon" :title="title" />
    <div class="category__stats">
      <div class="category__stats-item">
        <img src="../../assets/list.svg" alt="" width="20" height="20" />
        <span class="category__stats-number">{{ count }}</span>
      </div>
      <div class="category__stats-item">
        <img src="../../assets/done.svg" alt="" width="20" height="20" />
        <span class="category__stats-number">{{ done }}</span>
      </div>
      <div class="category__stats-item">
        <img src="../../assets/undone.svg" alt="" width="20" height="20" />
        <span class="category__stats-number">{{ undone }}</span>
      </div>
    </div>
  </div>
</template>

<script>
import SectionHeader from "../SectionHeader/SectionHeader.vue";

export default {
  name: "CategoryTitle",
  props: {
    icon: String,
    title: String,
    count: Number,
    done: Number,
    undone: Number,
  },
  components: {
    SectionHeader,
  },
};
</script>

<style lang="scss">
.category {
  &__title {
    color: #37352f;
    margin: 1rem 0;
  }

  &__stats {
    margin-top: 0.5rem;
    display: flex;
    align-items: center;
    gap: 1rem;

    &-item {
      display: flex;
      align-items: center;
      justify-items: flex-start;
      gap: 1rem;
      border-radius: 50px;
      padding: 3px;
      background: #eeeeee;
    }
    &-number {
      color: #37352f;
      font-style: italic;
    }
  }
}
</style>
