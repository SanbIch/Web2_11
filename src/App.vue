<template>
  <div id="app">
    <Header :mode="mode" @toggle="toggle" />
    <div class="main-сontainer">
      <button
        type="button"
        class="main-сontainer__create-task-btn"
        @click="showModal"
      >
        Создать задачу
      </button>
      <CreateTaskWind
        ref="modal"
        v-on:returned="addNewTask($event)"
        :action="action"
        :newTask="newTask"
        :mode="mode"
      ></CreateTaskWind>
      <div class="columns">
        <div
          class="columns-column"
          :class="
            mode == 'light' ? 'columns-column_light' : 'columns-column_dark'
          "
        >
          <h2 class="columns-column__column-title">
            {{ columns[0].title }} ({{ columns[0].plan.length }})
          </h2>
          <TaskCard
            :tasks="columns[0].plan"
            columnName="plan"
            left=""
            right="righttoInWork"
            v-on:move="moveTask($event)"
            v-on:showModal="showEditModal($event)"
            :mode="mode"
          ></TaskCard>
        </div>
        <div
          class="columns-column"
          :class="
            mode == 'light' ? 'columns-column_light' : 'columns-column_dark'
          "
        >
          <h2 class="columns-column__column-title">
            {{ columns[1].title }} ({{ columns[1].inWork.length }})
          </h2>
          <TaskCard
            :tasks="columns[1].inWork"
            columnName="inWork"
            left="lefttoPlan"
            right="rignttoDone"
            v-on:move="moveTask($event)"
            v-on:showModal="showEditModal($event)"
            :mode="mode"
          ></TaskCard>
        </div>
        <div
          class="columns-column"
          :class="
            mode == 'light' ? 'columns-column_light' : 'columns-column_dark'
          "
        >
          <h2 class="columns-column__column-title">
            {{ columns[2].title }} ({{ columns[2].Done.length }})
          </h2>
          <TaskCard
            :tasks="columns[2].Done"
            columnName="Done"
            left="lefttoInWork"
            right="rightdoneTask"
            v-on:move="moveTask($event)"
            v-on:showModal="showEditModal($event)"
            :mode="mode"
          ></TaskCard>
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
      mode: "light",
      nextid: 8,
      action: "",
      newTask: {
        desc: null,
        priority: "выберите приоритет",
        columnName: null,
        index: null,
      },
      columns: [
        {
          title: "План",
          plan: [
            {
              id: 7,
              desc: "Lorem ваыsum dolor sit amet consectetur adipisicing elit.",
              date: "14.14.1414 14:14:25",
              priority: 1,
            },
            {
              id: 6,
              desc: "Lorem ipsum dolor sit amet consectetur adipisicing elit",
              date: "14.14.1414 14:14:25",
              priority: 2,
            },
            {
              id: 5,
              desc: "Lorem ipsum dolor sit amet consectetur adipisicing elit.",
              date: "14.14.1414 14:14:25",
              priority: 3,
            },
          ],
        },
        {
          title: "В работе",
          inWork: [
            {
              id: 4,
              desc: "Lorem ipsum dolor sit amet consectetur adipisicing elit.",
              date: "14.14.1414 14:14:25",
              priority: 1,
            },
            {
              id: 3,
              desc: "Lorem ipsum dolor sit amet consectetur adipisicing elit.",
              date: "14.14.1414 14:14:25",
              priority: 2,
            },
          ],
        },
        {
          title: "Готово",
          Done: [
            {
              id: 2,
              desc: "Lorem ipsum dolor sit amet consectetur adipisicing elit.",
              date: "14.14.1414 14:14:25",
              priority: 1,
            },
            {
              id: 1,
              desc: "Lorem ipsum dolor sit amet consectetur adipisicing elit.",
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
      this.action = "add";
      this.$refs.modal.show = true;
      this.newTask.desc = null;
      this.newTask.index = null;
      this.newTask.priority = "выберите приоритет";
      this.newTask.columnName = null;
    },
    toggle() {
      if (this.mode === "dark") {
        this.mode = "light";
        document.body.classList.remove("bg-dark");
      } else {
        this.mode = "dark";
        document.body.classList.add("bg-dark");
      }
    },
    addNewTask(task) {
      switch (task.action) {
        case "add":
          this.columns[0].plan.unshift({
            id: this.nextid,
            desc: task.desc,
            date: task.date,
            priority: task.priority,
          });
          this.nextid++;
          break;
        case "edit":
          if (task.columnName == "plan") {
            this.columns[0].plan[task.index].desc = task.desc;
            this.columns[0].plan[task.index].date = task.date;
            this.columns[0].plan[task.index].priority = task.priority;
          } else if (task.columnName == "inWork") {
            this.columns[1].inWork[task.index].desc = task.desc;
            this.columns[1].inWork[task.index].date = task.date;
            this.columns[1].inWork[task.index].priority = task.priority;
          } else if (task.columnName == "done") {
            this.columns[2].Done[task.index].desc = task.desc;
            this.columns[2].Done[task.index].date = task.date;
            this.columns[2].Done[task.index].priority = task.priority;
          }
      }
    },
    moveTask(task) {
      switch (task.direction) {
        case "righttoInWork":
          this.columns[0].plan.splice(task.index, 1);
          this.columns[1].inWork.unshift(task.element);
          break;

        case "lefttoPlan":
          this.columns[1].inWork.splice(task.index, 1);
          this.columns[0].plan.unshift(task.element);
          break;

        case "rignttoDone":
          this.columns[1].inWork.splice(task.index, 1);
          this.columns[2].Done.unshift(task.element);
          break;

        case "lefttoInWork":
          this.columns[2].Done.splice(task.index, 1);
          this.columns[1].inWork.unshift(task.element);
          break;

        case "rightdoneTask":
          this.columns[2].Done.splice(task.index, 1);
          break;
      }
    },
    showEditModal(task) {
      this.action = "edit";
      this.$refs.modal.show = true;
      this.newTask.desc = task.element.desc;
      this.newTask.priority = task.element.priority;
      this.newTask.columnName = task.columnName;
      this.newTask.index = task.index;
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Montserrat:wght@400;500;700&display=swap");
.bg-dark {
  background-color: rgb(97, 97, 97);
  transition: background-color 0.5s ease-in-out;
}
.main-сontainer {
  padding: 0 15%;
}
.main-сontainer__create-task-btn {
  padding: 10px;
  background-color: #219afb;
  border: none;
  color: white;
  cursor: pointer;
}
.main-сontainer__create-task-btn:hover {
  background-color: #218fe9;
}
.main-сontainer__create-task-btn:active {
  transform: scale(0.95, 0.95);
}
.columns {
  display: flex;
  justify-content: space-between;
}
.columns-column {
  padding: 0 20px;
  width: 26%;
  transition: background-color 0.5s ease-in-out;
}
.columns-column_light {
  background-color: #f1f9ff;
  color: black;
}
.columns-column_dark {
  background-color: rgb(70, 70, 70);
  color: white;
}
.columns-column__column-title {
  text-align: center;
}
body {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Montserrat", sans-serif;
}
.ghost-card {
  opacity: 0.5;
  background: #f7fafc;
  border: 1px solid #4299e1;
}
</style>
