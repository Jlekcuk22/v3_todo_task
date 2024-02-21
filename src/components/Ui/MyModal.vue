<template>
  <div class="modal" v-if="show" @click="hideModal">
    <div @click.stop class="modal_content">
      <slot></slot>
    </div>
  </div>
</template>
<script>
export default {
  name: "my-modal",
  props: {
    show: {
      type: Boolean,
      default: false,
    },
  },
  methods: {
    hideModal() {
      this.$emit("update:show", false);
    },
  },
};
</script>

<style scoped>
.modal {
  position: fixed;
  display: flex;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: rgba(0, 0, 0, 0.7);
}

.modal_content {
  margin: auto;
  background: white;
  border-radius: 10px;
  min-width: 350px;
  min-height: 50px;
  padding: 10px;
}
</style>
