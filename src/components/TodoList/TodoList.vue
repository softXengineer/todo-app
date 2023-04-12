<template>
  <div class="todo__list flex-column">
    <TodoListItem
      v-for="task in tasks"
      :key="task.id"
      :task="task"
      :deleteTask="deleteTask"
      :addTask="addTask"
      :updateTask="updateTask"
    />
  </div>
</template>

<script>
import TodoListItem from "../TodoListItem/TodoListItem.vue";
export default {
  name: "TodoList",
  components: {
    TodoListItem,
  },
  props: {
    tasks: Array,
    deleteTask: Function,
    addTask: Function,
    updateTask: Function,
  },
};
</script>

<style lang="scss">
.todo {
  &__list {
    display: flex;
    width: 100%;
    gap: 0.2rem;
    max-height: 70vh;
    overflow-y: scroll;
    &.flex-column {
      flex-direction: column;
    }
  }
}
</style>
