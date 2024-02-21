<template>
  <div class="app">
    <h1>Страница задач</h1>
    <div class="app_btns mt-15">
      <my-button @click="showModal">Создать задачу</my-button>
      <my-select v-model="selectedFilter" :options="filterOptions"></my-select>
    </div>

    <my-modal v-model:show="modalVisible">
      <task-form @create="createTask" />
    </my-modal>

    <task-list
      :tasks="filteredTasks"
      @remove="removeTask"
      v-if="!isTaskLoading"
    />
    <div class="mt-15" v-else>Загрузка задач...</div>
  </div>
</template>
<script>
import TaskForm from "./components/TaskForm.vue";
import TaskList from "./components/TaskList.vue";
import axios from "axios";
import MySelect from "./components/Ui/MySelect.vue";

export default {
  components: {
    TaskForm,
    TaskList,
    MySelect,
  },
  data() {
    return {
      tasks: [],
      modalVisible: false,
      isTaskLoading: false,
      selectedFilter: "",
      filterOptions: [
        { value: "", name: "Все" },
        { value: "false", name: "Завершенные" },
        { value: "true", name: "В процессе" },
      ],
    };
  },
  methods: {
    createTask(task) {
      this.tasks.push(task);
      this.modalVisible = false;
    },
    removeTask(task) {
      this.tasks = this.tasks.filter((t) => t.id !== task.id);
    },

    showModal() {
      this.modalVisible = true;
    },

    async fetchTasks() {
      try {
        this.isTaskLoading = true;
        const response = await axios.get(
          "https://jsonplaceholder.typicode.com/todos?_limit=10"
        );
        this.tasks = response.data;
        this.isTaskLoading = false;
      } catch (e) {
        alert("Ошибка");
      }
    },
  },
  computed: {
    filteredTasks() {
      if (this.selectedFilter === "") {
        return this.tasks;
      } else {
        return this.tasks.filter(
          (task) => task.completed.toString() === this.selectedFilter
        );
      }
    },
  },
  mounted() {
    this.fetchTasks();
  },
};
</script>
<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.app {
  padding: 15px;
}

.app_btns {
  display: flex;
  justify-content: space-between;
}

.mt-15 {
  margin-top: 15px;
}
</style>
