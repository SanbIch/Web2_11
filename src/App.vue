<template>
  <div id="app">
    <Header />
    <div class="mainContainer">
      <button type="button" class="createTaskBtn" @click="showModal">
        Создать задачу
      </button>
      <CreateTaskWind ref="modal"></CreateTaskWind>
      <div class="columns">
        <div v-for="column in columns" :key="column.title" class="column">
          <h2 class="columnTitle">
            {{ column.title }} ({{ column.tasks.length }})
          </h2>
          <TaskCard></TaskCard>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import TaskCard from "./components/TaskCard.vue";
import Header from "./components/Header.vue";
import CreateTaskWind from "./components/CreateTaskWind.vue";
export default {
  name: "App",
  components: {
    TaskCard,
    Header,
    CreateTaskWind,
  },
  data() {
    return {
      columns: [
        {
          title: "План",
          tasks: [
            {
              id: 1,
              date: "14.14.1414 14:14:25",
              priority: 1,
            },
            {
              id: 2,
              date: "14.14.1414 14:14:25",
              priority: 2,
            },
            {
              id: 3,
              date: "14.14.1414 14:14:25",
              priority: 3,
            },
          ],
        },
        {
          title: "В работе",
          tasks: [
            {
              id: 3,
              date: "14.14.1414 14:14:25",
              priority: 1,
            },
            {
              id: 4,
              date: "14.14.1414 14:14:25",
              priority: 2,
            },
          ],
        },
        {
          title: "Готово",
          tasks: [
            {
              id: 5,
              date: "14.14.1414 14:14:25",
              priority: 1,
            },
            {
              id: 6,
              date: "14.14.1414 14:14:25",
              priority: 2,
            },
          ],
        },
      ],
    };
  },
  methods: {
    showModal: function () {
      this.$refs.modal.show = true;
    },
  },
};
</script>

<style>
.mainContainer {
  padding: 0 15%;
}
.createTaskBtn {
  padding: 10px;
  background-color: #219afb;
  border: none;
  color: white;
  cursor: pointer;
}
.createTaskBtn:hover {
  background-color: #218fe9;
}
.createTaskBtn:active {
  transform: scale(0.95, 0.95);
}
.columnTitle {
  text-align: center;
}
.columns {
  display: flex;
  justify-content: space-between;
}
.column {
  background-color: #f1f9ff;
  padding: 0 20px;
  width: 26%;
}
body {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.ghost-card {
  opacity: 0.5;
  background: #f7fafc;
  border: 1px solid #4299e1;
}
</style>
