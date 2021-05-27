<template>
  <div id="app">
    <TaskList
      v-bind:tasks="tasksData"
      :showCompletedTasks="false"
      v-on:add-task="addTask"
      v-on:remove-task="removeTask"
    ></TaskList>
    <TaskList v-bind:tasks="tasksData" :showCompletedTasks="true"></TaskList>
  </div>
</template>

<script>
import TaskList from "@/components/TaskList";
import axios from "axios";

export default {
  name: "App",
  components: {
    TaskList,
  },
  methods: {
    addTask() {
      function calculateTaskSequence(tasksData) {
        var remTasks = tasksData.filter((task) => !task.completed);
        return remTasks === undefined ? 1 : remTasks.length + 1;
      }

      const newTask = {
        completed: false,
        title:
          this.tasksData === 0
            ? "Task 1"
            : "Task " + (this.tasksData.length + 1),
        sequence: calculateTaskSequence(this.tasksData),
      };

      axios
        .post("http://185.246.66.84:3000/llerman/tasks", newTask)
        .then((response) => {
          this.tasksData = [...this.tasksData, response.data];
        });
    },
    removeTask(id) {
      axios
        .delete("http://185.246.66.84:3000/llerman/tasks/" + id)
        .then(() => {
          this.tasksData = this.tasksData.filter((task) => task.id !== id);
        })
        .catch((error) => console.log(error));
    },
  },
  data() {
    return {
      tasksData: [],
    };
  },
  mounted() {
    axios
      .get("http://185.246.66.84:3000/llerman/tasks")
      .then((response) => {
        this.tasksData = response.data;
      })
      .catch((error) => console.log(error));
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 60px;
}
</style>
