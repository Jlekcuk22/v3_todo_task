<template>
  <div class="task">
    <div>
      <div><b>Название:</b>{{ task.title }}</div>
      <div>
        <b class="mr-5">Статус:</b>
        <strong :class="task.completed ? 'green' : 'red'">
          {{ task.completed ? "Завершена" : "В процессе" }}
        </strong>
      </div>
    </div>
    <div class="taskBtns">
      <my-button @click="showModal" class="mr-5"> Редактировать </my-button>
      <my-button @click="$emit('remove', task)">Удалить</my-button>
    </div>
    <my-modal v-model:show="modalVisible">
      <edit-form @edit="editTask" :title="task.title" />
    </my-modal>
  </div>
</template>
<script>
import EditForm from "./EditForm.vue";

export default {
  components: { EditForm },
  props: {
    task: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      modalVisible: false,
    };
  },
  methods: {
    editTask(task) {
      this.isEditing = true;
      this.modalVisible = false;
      this.task.title = task.title;
    },
    showModal() {
      this.modalVisible = true;
    },
    saveChanges() {
      this.$emit("save", this.editedTask);
    },
  },
};
</script>

<style scoped>
.task {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px;
  border: 1.5px solid darkcyan;
  margin-top: 10px;
}

.taskBtns {
  display: flex;
  justify-content: space-between;
}

.green {
  color: green;
}
.red {
  color: red;
}

.mr-5 {
  margin-right: 5px;
}
</style>
