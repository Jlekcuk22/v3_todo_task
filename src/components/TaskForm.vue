<template>
  <form @submit.prevent class="form">
    <h4>Создание задачи</h4>
    <my-input v-model="task.title" type="text" placeholder="Название" />
    <my-button class="mt-15" @click="createTask">Создать</my-button>
  </form>
</template>
<script>
export default {
  data() {
    return {
      task: {
        title: "",
        completed: "",
      },
    };
  },
  methods: {
    createTask() {
      this.task.id = Date.now();
      this.$emit("create", this.task);
      this.task = {
        title: "",
        completed: "",
      };
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
