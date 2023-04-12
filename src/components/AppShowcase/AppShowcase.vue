<template>
  <div class="showcase">
    <div class="showcase__inner">
      <CategoryTitle
        :title="selectedCategory.title"
        :icon="selectedCategory.icon"
        :done="selectedCategory.done"
        :undone="selectedCategory.undone"
        :count="selectedCategory.count"
      />
      <TodoList
        :tasks="selectedCategory.tasks"
        :deleteTask="deleteTask"
        :addTask="addTask"
        :updateTask="updateTask"
      />
      <div
        class="showcase__info"
        v-show="
          selectedCategory.tasks.length === 0 && selectedCategory.id !== 'none'
        "
      >
        Please create a task!
      </div>
      <TodoForm :selectedCategory="selectedCategory" :addTask="addTask" />
    </div>
  </div>
</template>

<script>
import CategoryTitle from "../CategoryTitle/CategoryTitle.vue";
import TodoList from "../TodoList/TodoList.vue";
import TodoForm from "../TodoForm/TodoForm.vue";

export default {
  name: "AppShowcase",
  components: {
    CategoryTitle,
    TodoList,
    TodoForm,
  },
  props: {
    selectedCategory: Object,
    deleteTask: Function,
    addTask: Function,
    updateTask: Function,
  },
};
</script>

<style lang="scss">
.showcase {
  width: 100%;
  padding: 2rem;
  min-height: 94vh;

  &__inner {
    height: 100%;
    position: relative;
  }
}
</style>
