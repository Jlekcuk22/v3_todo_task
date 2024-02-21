<template>
  <form @submit.prevent class="form">
    <h4>Редактирование задачи</h4>
    <my-input v-model="task.title" type="text" placeholder="Название" />
    <my-button class="mt-15" @click="$emit('edit', task)">Сохранить</my-button>
  </form>
</template>
<script>
export default {
  data() {
    return {
      task: {
        title: this.$props.title,
        completed: "",
      },
      modalVisible: false,
    };
  },
  props: ["title"],
  methods: {
    editTask(task) {
      this.editTask = { ...task };
      this.isEditing = true;
      this.modalVisible = true;
    },
  },
};
</script>
<style scoped>
.form {
  display: flex;
  flex-direction: column;
}
</style>
