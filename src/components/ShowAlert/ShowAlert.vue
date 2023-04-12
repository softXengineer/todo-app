<template>
  <div class="alert">
    <img v-if="type === 'success'" src="../../assets/done.svg" alt="Success" />
    <img v-else-if="type === 'info'" src="../../assets/info.svg" alt="info" />
    <img v-else src="../../assets/warning.svg" alt="Error" />
    {{ message }}
  </div>
</template>

<script>
export default {
  name: "ShowAlert",
  props: {
    type: String,
    message: String,
  },
};
</script>

<style lang="scss">
.alert {
  display: flex;
  align-items: center;
  gap: 1rem;
  position: fixed;
  top: 0px;
  background-color: #fff;
  padding: 1.2rem;
  font-size: 16px;
  z-index: 20;
  border-bottom-left-radius: 0.8rem;
  border-bottom-right-radius: 0.8rem;
  left: 50%;
  transform: translateX(-50%);
  box-shadow: 0 2px 10px 5px #00000010;
  animation: anim 0.2s ease forwards;
  img {
    width: 28px;
  }
  @keyframes anim {
    from {
      transform: translateX(-50%) scale(0.5);
    }
    to {
      transform: translateX(-50%) scale(1);
    }
  }
}
</style>
