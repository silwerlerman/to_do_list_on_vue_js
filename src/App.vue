<template>
  <div id="app">
    <TaskList v-bind:tasks="tasksData" :showCompletedTasks="false"></TaskList>
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
  color: #2c3e50;
  margin-top: 60px;
}
</style>
