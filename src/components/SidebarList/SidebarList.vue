<template>
  <div class="sidebar__list flex-column">
    <SidebarListItem
      v-for="category in categories"
      :key="category.id"
      :category="category"
      :deleteCategory="deleteCategory"
      :selectCategory="selectCategory"
      :selectedCategory="selectedCategory"
    />
  </div>
</template>

<script>
import SidebarListItem from "../SidebarListItem/SidebarListItem.vue";
export default {
  name: "SidebarList",
  components: {
    SidebarListItem,
  },
  props: {
    categories: Array,
    deleteCategory: Function,
    selectCategory: Function,
    selectedCategory: Object,
  },
};
</script>

<style lang="scss">
.sidebar {
  &__list {
    margin-bottom: 15px;
    display: flex;
    width: 100%;
    gap: 0.2rem;
    max-height: 80vh;
    overflow-y: scroll;
    &.flex-column {
      flex-direction: column;
    }
  }
}
</style>
