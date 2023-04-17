<template>
  <header>
    <button
      :class="[!isMenuOpen && 'close', 'close-btn']"
      @click="openSidebarHandler"
    >
      <span>&#10005;</span>
    </button>
  </header>
</template>

<script>
export default {
  name: "AppHeader",
  props: {
    isMenuOpen: Boolean,
    openSidebarHandler: Function,
  },
};
</script>

<style lang="scss">
header {
  background: #f0f0f0;
  min-height: 6vh;
  padding: 0 2rem;
  display: flex;
  align-items: center;

  .close-btn {
    font-size: 1.5rem;
    border: none;
    outline: none;
    background: transparent;
    color: #000;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    width: 25px;
    height: 25px;
    cursor: pointer;
    user-select: none;
    transition: transform 0.3s ease;
    &.close {
      transform: rotate(45deg);
    }
  }
}
</style>
