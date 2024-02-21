<template>
  <div class="mt-15" v-if="tasks.length > 0">
    <h3>Список задач</h3>
    <transition-group name="task-list">
      <task-item
        v-for="task in tasks"
        :task="task"
        :key="task.id"
        @remove="$emit('remove', task)"
      />
    </transition-group>
  </div>
  <div v-else>
    <h2 style="color: lightcoral">На данный момент нет задач</h2>
  </div>
</template>
<script>
import TaskItem from "./TaskItem.vue";
export default {
  components: {
    TaskItem,
  },
  props: {
    tasks: {
      type: Array,
      required: true,
    },
  },
};
</script>
<style scoped>
.task-list-item {
  display: inline-block;
  margin-right: 10px;
}
.task-list-enter-active,
.task-list-leave-active {
  transition: all 0.4s ease;
}
.task-list-enter-from,
.task-list-leave-to {
  opacity: 0;
  transform: translateX(130px);
}
.task-list-move {
  transition: transform 0.4s ease;
}
</style>
