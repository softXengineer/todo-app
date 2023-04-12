<template>
  <form @submit="onSubmit" class="todo__form">
    <div class="todo__form-holder">
      <input type="text" placeholder="+ Add a task" v-model="value" />
      <button>&#x25B2;</button>
    </div>
  </form>
</template>

<script>
export default {
  name: "TodoForm",
  props: {
    categories: Array,
    addTask: Function,
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
        const newTask = {
          id,
          title: this.value,
          status: false,
        };

        // addTask(newTask);
        this.addTask(newTask);
        this.value = "";
        // setCategories([...categories, newCategory]);
        // setSelectedCategory(newCategory);
      }
    },
  },
};
</script>

<style lang="scss">
.todo {
  &__form {
    position: absolute;
    width: 100%;
    bottom: 1rem;

    &-holder {
      width: 100%;
      display: flex;
      align-items: center;
      position: relative;

      input {
        width: 100%;
        padding: 0.6rem;
        font-size: 1rem;
        color: #444;
        border: none;
        border-radius: 6px;
        outline: none;
        background-color: #eee;
        &:hover {
          background-color: #fef;
        }
      }

      button {
        position: absolute;
        right: 10px;
        border: none;
        outline: none;
        background-color: transparent;
        color: #333;
        font-size: 1.1rem;
        z-index: 2;
        cursor: pointer;
      }
    }
  }
}
</style>
