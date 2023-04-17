<template>
  <div :class="[isMenuOpen ? 'open' : 'close', 'sidebar']">
    <div class="sidebar__inner">
      <SidebarList
        :categories="categories"
        :deleteCategory="deleteCategory"
        :selectCategory="selectCategory"
        :selectedCategory="selectedCategory"
      />
      <div class="sidebar__info" v-show="categories.length === 0">
        Please create a catgeory!
      </div>
      <SidebarForm :addCategory="addCategory" :showAlert="showAlert" />
    </div>
  </div>
</template>

<script>
import SidebarList from "../SidebarList/SidebarList.vue";
import SidebarForm from "../SidebarForm/SidebarForm.vue";

export default {
  name: "AppSidebar",
  components: {
    SidebarList,
    SidebarForm,
  },
  props: {
    isMenuOpen: Boolean,
    categories: Array,
    addCategory: Function,
    deleteCategory: Function,
    selectCategory: Function,
    selectedCategory: Object,
    showAlert: Function,
  },
  data() {
    return {
      value: "",
    };
  },
  methods: {
    onSubmit(event) {
      event.preventDefault();
      if (this.value) {
        const id = new Date().getTime();
        const newCategory = {
          id,
          count: 0,
          title: this.value,
          icon: "💥",
          tasks: [],
        };
        this.$emit("add-category", newCategory);

        this.value = "";
      }
    },
  },
};
</script>

<style lang="scss">
.sidebar {
  width: 30%;
  padding: 2rem 1rem;
  background-color: #fbfbfa;
  min-height: 94vh;
  position: relative;
  transition: left 0.3s ease;

  &.open {
    left: 0;
  }
  &.close {
    left: -100%;
    width: 0;
  }

  &__inner {
    height: 100%;
    position: relative;
  }

  &__info {
    text-align: center;
  }
}

@media (min-width: 0px) and (max-width: 768px) {
  .sidebar {
    width: 100%;
    position: absolute;
    z-index: 10;
    &__inner {
      min-height: 87vh;
    }
  }
}
@media (min-width: 768px) and (max-width: 1200px) {
  .sidebar {
    width: 100%;
  }
}
</style>
