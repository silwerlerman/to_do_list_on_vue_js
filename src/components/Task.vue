<template>
  <div
    v-bind:class="{
      item: true,
      todo: !task.completed,
      completed: task.completed,
    }"
  >
    <div v-bind:class="{ items: true }">
      <input
        v-bind:class="{ checkbox: true }"
        type="checkbox"
        :checked="task.completed"
      />
      <p v-bind:class="{ text: true, inputLineThrough: task.completed }">
        {{ task.title }}
      </p>
    </div>
    <div>
      <button v-if="task.completed">Восстановить</button>
      <button v-if="!task.completed">Редактировать</button>
      <button v-if="!task.completed" v-on:click="$emit('remove-task', task.id)">
        Удалить
      </button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    task: {
      type: Object,
      require: true,
    },
  },
};
</script>

<style scope>
.item {
  display: flex;
  justify-content: space-between;
  margin: 5px;
  padding: 5px;
  min-width: 300px;
}
.items {
  display: flex;
  flex-direction: row;
}
.todo {
  border: 2px double green;
}
.completed {
  border: 2px double red;
}
.checkbox {
  text-decoration: line-through;
}
.input {
  border: 0px;
  text-decoration-color: black;
}
.inputLineThrough {
  text-decoration: line-through;
}
.text {
  margin: 0px;
  margin-left: 5px;
}
</style>