<template>
  <div
    :class="[selectedCategory.id === category.id && 'active', 'sidebar__item']"
    @click="selectCategory(category)"
  >
    <div class="sidebar__item-main">
      <div class="sidebar__icon">{{ category.icon }}</div>
      {{ category.title }}
    </div>
    <div class="sidebar__item-secondary">
      <div class="sidebar__count">{{ category.count }}</div>
      <div @click="deleteCategory(category.id)" class="delete-category">
        &#10005;
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "SidebarListItem",
  props: {
    category: Object,
    deleteCategory: Function,
    selectCategory: Function,
    selectedCategory: Object,
  },
};
</script>

<style lang="scss">
.sidebar {
  &__item {
    display: flex;
    width: 100%;
    gap: 0.5rem;
    align-items: center;
    padding: 0.5rem;
    border-radius: 6px;
    cursor: pointer;

    &.active {
      background: #96b996; /* fallback for old browsers */
      background: -webkit-linear-gradient(
        to right,
        #c5f8c5,
        #fcd9d9
      ); /* Chrome 10-25, Safari 5.1-6 */
      background: linear-gradient(
        to right,
        #bcebbc,
        #e2c0c0
      ); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */

      &:hover {
        background: #8aaa8a; /* fallback for old browsers */
        background: -webkit-linear-gradient(
          to right,
          #bbf5bb,
          #fcd1d1
        ); /* Chrome 10-25, Safari 5.1-6 */
        background: linear-gradient(
          to right,
          #b8ebb8,
          #dfb7b7
        ); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
      }
    }

    &:hover {
      background: #abbaab; /* fallback for old browsers */
      background: -webkit-linear-gradient(
        to right,
        #e2f4e2,
        #f5eded
      ); /* Chrome 10-25, Safari 5.1-6 */
      background: linear-gradient(
        to right,
        #e2f4e2,
        #f5eded
      ); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
    }
    &-main {
      display: flex;
      gap: 0.6rem;
      align-items: center;
      margin-right: 10px;
      flex: 1;
    }
    &-secondary {
      display: flex;
      gap: 1rem;
      align-items: center;
      justify-content: flex-end;
    }
  }
  &__icon {
    font-size: 1.2rem;
  }
  &__count {
    color: #666;
    width: 20px;
    text-align: right;
  }
  .delete-category {
    user-select: none;
  }
  .delete-category:hover {
    color: rgb(223, 0, 0);
  }
}
</style>
