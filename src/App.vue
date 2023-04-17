<template>
  <div id="app">
    <ShowAlert v-show="alertOpen" :type="alertType" :message="message" />
    <AppHeader :openSidebarHandler="openSidebarHandler" :isMenuOpen="isMenuOpen" />
    <main>
      <AppSidebar
        :categories="categories"
        :addCategory="addCategory"
        :selectCategory="selectCategory"
        :deleteCategory="deleteCategory"
        :selectedCategory="selectedCategory"
        :showAlert="showAlert"
        :isMenuOpen="isMenuOpen"
      />
      <AppShowcase
        :selectedCategory="selectedCategory"
        :addTask="addTask"
        :updateTask="updateTask"
        :deleteTask="deleteTask"
      />
    </main>
  </div>
</template>

<script>
import AppHeader from "./components/AppHeader/AppHeader.vue";
import AppSidebar from "./components/AppSidebar/AppSidebar.vue";
import AppShowcase from "./components/AppShowcase/AppShowcase.vue";
import ShowAlert from "./components/ShowAlert/ShowAlert.vue";

export default {
  name: "App",
  components: {
    AppHeader,
    AppSidebar,
    AppShowcase,
    ShowAlert,
  },
  data() {
    return {
      isMenuOpen: true,
      alertOpen: false,
      alertType: "success",
      message: "",
      categories: [],
      selectedCategory: {
        id: "none",
        count: 0,
        icon: "🥺",
        title: "Please select a category!",
        tasks: [],
      },
    };
  },
  created() {
    this.categories = [
      {
        id: 0,
        count: 0,
        icon: "🧘‍♂️",
        title: "Personal Development",
        tasks: [],
        done: 0,
        undone: 0,
      },
      {
        id: 1,
        count: 0,
        icon: "🏢",
        title: "Work",
        tasks: [],
        done: 0,
        undone: 0,
      },
    ];
  },
  methods: {
    openSidebarHandler() {
      this.isMenuOpen = !this.isMenuOpen;
    },
    showAlert(type, message) {
      this.alertOpen = true;
      this.alertType = type;
      this.message = message;

      setTimeout(() => {
        this.alertOpen = false;
        this.alertType = "success";
        this.message = "";
      }, 5000);
    },
    addCategory(category) {
      this.categories = [...this.categories, category];
      this.selectedCategory = category;
    },
    selectCategory(category) {
      if (window.screen.width < 768) {
        this.isMenuOpen = !this.isMenuOpen;
      }
      this.selectedCategory = category;
    },
    deleteCategory(id) {
      this.categories = this.categories.filter(
        (category) => category.id !== id
      );
      if (this.categories.length === 0) {
        this.selectedCategory = {
          id: "none",
          title: "There is no categories!",
          icon: "🤬",
          tasks: [],
        };
      }
      if (this.selectedCategory.id === id) {
        this.selectedCategory = this.categories[0];
      }
      this.showAlert("success", "Category deleted successfuly!");
    },
    addTask(task) {
      if (this.selectedCategory.id === "none")
        return this.showAlert("error", "Please select a category!");

      const tasks = [...this.selectedCategory.tasks, task];
      const newSelected = {
        ...this.selectedCategory,
        tasks,
        count: tasks.length,
        undone: this.selectedCategory.undone + 1,
      };

      this.categories = this.categories.map((category) =>
        category.id === this.selectedCategory.id ? newSelected : category
      );

      this.selectedCategory = newSelected;
    },
    deleteTask(id) {
      const tasks = this.selectedCategory.tasks.filter(
        (task) => task.id !== id
      );
      const done = tasks.filter((t) => t.status).length;
      const undone = tasks.filter((t) => !t.status).length;

      const newSelected = {
        ...this.selectedCategory,
        tasks,
        count: tasks.length,
        done,
        undone,
      };

      const newCategories = this.categories.map((category) =>
        category.id === this.selectedCategory.id ? newSelected : category
      );

      this.selectedCategory = newSelected;
      this.categories = newCategories;
    },
    updateTask(task) {
      const tasks = this.selectedCategory.tasks.map((t) =>
        t.id === task.id ? task : t
      );
      const done = tasks.filter((t) => t.status).length;
      const undone = tasks.filter((t) => !t.status).length;
      const newSelected = {
        ...this.selectedCategory,
        tasks,
        done,
        undone,
      };

      this.categories = this.categories.map((category) =>
        category.id === this.selectedCategory.id ? newSelected : category
      );
      this.selectedCategory = newSelected;
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html {
  font-family: "Jost", sans-serif;
}

body {
  margin: 0;
  font-family: "Jost", -apple-system, BlinkMacSystemFont, "Segoe UI", "Roboto",
    "Oxygen", "Ubuntu", "Cantarell", "Fira Sans", "Droid Sans", "Helvetica Neue",
    sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

main {
  width: 100%;
  display: flex;
}

svg,
i {
  pointer-events: none;
}

*::-webkit-scrollbar {
  width: 3px;
}

*::-webkit-scrollbar-track {
  background: transparent;
}

*::-webkit-scrollbar-thumb {
  background-color: rgba(155, 155, 155, 0.5);
  border-radius: 2px;
  border: transparent;
}
</style>
