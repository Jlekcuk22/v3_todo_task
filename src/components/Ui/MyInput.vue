<template>
  <input :value="modelValue" @input="updateInput" class="inp" type="text" />
</template>

<script>
export default {
  name: "my-input",
  props: {
    modelValue: {
      type: [String, Number],
    },
  },
  methods: {
    updateInput(event) {
      this.$emit("update:modelValue", event.target.value);
    },
  },
};
</script>

<style scoped>
.inp {
  width: 100%;
  border: 1px solid darkcyan;
  padding: 5px 10px;
  margin-top: 10px;
}
</style>
