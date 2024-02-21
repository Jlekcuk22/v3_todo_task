<template>
  <button class="btn">
    <slot></slot>
  </button>
</template>
<script>
export default {
  name: "my-button",
};
</script>
<style scoped>
.btn {
  align-self: end;
  background: none;
  padding: 7px 15px;
  color: darkcyan;
  border: 1px solid darkcyan;
  border-radius: 8px;
}
</style>
