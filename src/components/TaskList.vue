<template>
  <div v-bind:class="{ form: true }">
    <div v-bind:class="{ list: true }">
      <div>
        <h2>
          {{ showCompletedTasks ? "Завершенные задачи" : "Текущие задачи" }}
        </h2>
        <div v-if="!showCompletedTasks" v-bind:class="{ addButton: true }">
          <button v-on:click="$emit('add-task')">Добавить</button>
        </div>
      </div>
      <Task v-for="task in filterTasks" v-bind:task="task" :key="task.id" />
    </div>
  </div>
</template>

<script>
import Task from "@/components/Task";
export default {
  props: {
    tasks: Array,
    showCompletedTasks: Boolean,
  },
  components: {
    Task,
  },
  computed: {
    filterTasks() {
      return this.showCompletedTasks
        ? this.tasks.filter((task) => task.completed)
        : this.tasks.filter((task) => !task.completed);
    },
  },
};
</script>

<style scope>
.list {
  min-width: 400px;
}
.form {
  display: flex;
  flex-direction: column;
  align-items: center;
  align-content: center;
}
.addbutton {
  display: flex;
  justify-content: center;
  margin-bottom: 25px;
}
</style>