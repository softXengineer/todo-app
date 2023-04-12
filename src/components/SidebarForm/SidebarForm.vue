<template>
  <form @submit="onSubmit" class="sidebar__form">
    <div class="sidebar__form-icon">
      <input type="text" v-model="icon" @click="openEmojiPanel" />
    </div>
    <div class="sidebar__form-holder">
      <input type="text" placeholder="+ Add a category" v-model="value" />
      <button>&#x25B2;</button>
    </div>
  </form>
</template>

<script>
export default {
  name: "SidebarForm",
  props: {
    categories: Array,
    addCategory: Function,
    showAlert: Function,
  },
  data() {
    return {
      value: "",
      icon: "😁",
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
          icon: this.icon,
          tasks: [],
          done: 0,
          undone: 0,
        };
        this.addCategory(newCategory);

        this.value = "";
        this.icon = "🫡";
      }
    },
    openEmojiPanel() {
      if (navigator.platform.indexOf("Mac") === 0) {
        this.showAlert(
          "info",
          "Please use this command: Command + Control + Space"
        );
      } else if (navigator.platform.indexOf("Win") === 0) {
        this.showAlert(
          "info",
          "Please use this command:  Windows logo key + ."
        );
      }
      this.icon = "";
    },
  },
};
</script>

<style lang="scss">
.sidebar {
  &__form {
    display: flex;
    align-items: center;
    position: absolute;
    width: 100%;
    bottom: 0;

    &-icon {
      width: 10%;
      margin-right: 10px;

      input {
        width: 100%;
        display: block;
        border: none;
        outline: none;
        text-align: center;
        cursor: pointer;
        font-size: 1.2rem;
      }
    }
    &-holder {
      flex: 1;
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
