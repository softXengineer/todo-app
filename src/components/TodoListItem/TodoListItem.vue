<template>
  <div :class="[task.status && 'done', 'todo__item']">
    <div class="todo__item-main">
      <div class="todo__control">
        <input
          type="checkbox"
          :name="task.id"
          :id="task.id"
          v-model="checked"
          @change="updateHandler(task)"
        />
        <label
          :class="[task.status && 'done', 'todo__label']"
          v-bind:for="task.id"
        >
          {{ task.title }}
        </label>
      </div>
    </div>
    <div class="todo__item-secondary">
      <div @click="deleteTask(task.id)" class="delete-task">&#10005;</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "TodoListItem",
  props: {
    task: Object,
    deleteTask: Function,
    addTask: Function,
    updateTask: Function,
  },
  data() {
    return {
      checked: this.task.status,
    };
  },
  methods: {
    updateHandler(task) {
      this.updateTask({ ...task, status: !task.status });
    },
  },
};
</script>

<style lang="scss">
.todo {
  &__item {
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 0.5rem 1rem;
    border-radius: 6px;
    margin: 2px 0;
    cursor: pointer;
    transition: width 0.3s ease;

    &.done {
      background: #998e69; /* fallback for old browsers */
      background: -webkit-linear-gradient(
        to right,
        #ffffff,
        #837850
      ); /* Chrome 10-25, Safari 5.1-6 */
      background: linear-gradient(
        to right,
        #f0cccc,
        #e7d8a1
      ); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
      &:hover {
        background: #867c5c; /* fallback for old browsers */
        background: -webkit-linear-gradient(
          to right,
          #ffffff,
          #746a47
        ); /* Chrome 10-25, Safari 5.1-6 */
        background: linear-gradient(
          to right,
          #eec6c6,
          #e6d59a
        ); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
      }
    }

    &:hover {
      background: #ffefba; /* fallback for old browsers */
      background: -webkit-linear-gradient(
        to right,
        #ffffff,
        #ffefba
      ); /* Chrome 10-25, Safari 5.1-6 */
      background: linear-gradient(
        to right,
        #fff5f5,
        #fffbec
      ); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
    }

    &-main {
      flex: 1;
      margin-right: 10px;
    }

    &-secondary {
      display: flex;
      gap: 1rem;
      justify-content: flex-end;
    }
  }

  &__control {
    display: flex;
    gap: 0.5rem;
    align-items: center;
  }
  &__label {
    font-size: 1.2rem;
    color: #333;
    background-color: transparent;
    border: none;
    outline: none;

    &.done {
      color: #666;
      text-decoration: line-through;
      text-decoration-thickness: 2px;
      text-decoration-color: #555;
      font-style: italic;
    }

    &:hover {
      color: #000;
      display: block;
    }
  }
  .delete-task {
    user-select: none;
  }
  .delete-task:hover {
    color: rgb(223, 0, 0);
  }
}
</style>
