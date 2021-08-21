<template>
  <draggable :list="tasks" group="tasks" itemKey="name" ghost-class="ghost">
    <template #item="{ element, index }">
      <div class="taskCard" :class="mode == 'light' ? 'lightTask' : 'darkTask'">
        <div class="headerTask">
          <h3 class="headerTask__title">Задача №{{ element.id }}</h3>
          <badge
            :class="[
              element.priority == 1 ? 'firstPriority' : '',
              element.priority == 2 ? 'secondPriority' : '',
              element.priority == 3 ? 'thirdPriority' : '',
            ]"
            >{{ element.priority }}</badge
          >
        </div>
        <div class="descriptionTask">
          <p>{{ element.desc }}</p>
          <span>{{ element.date }}</span>
        </div>
        <div class="controls">
          <button
            :disabled="columnName == 'plan'"
            :class="[
              columnName == 'plan' ? 'disabledBtn' : '',
              mode == 'light' ? 'lightTask' : 'darkTask',
            ]"
            class="controlBtn left"
            @click="move(left, index, element)"
          >
            <img src="../assets/left-arrow.svg" alt="" />
          </button>
          <button
            class="controlBtn edit"
            :class="mode == 'light' ? 'lightTask' : 'darkTask'"
            @click="showModal(columnName, index, element)"
          >
            Edit
          </button>
          <button
            class="controlBtn right"
            :class="mode == 'light' ? 'lightTask' : 'darkTask'"
            @click="move(right, index, element)"
          >
            <img v-if="columnName == 'Done'" src="../assets/close.svg" alt="" />
            <img v-else src="../assets/right-arrow.svg" alt="" />
          </button>
        </div>
      </div>
    </template>
  </draggable>
</template>

<script>
import Badge from "./Badge.vue";
import draggable from "vuedraggable";
export default {
  components: {
    draggable,
    Badge,
  },
  props: {
    tasks: Object,
    columnName: String,
    left: String,
    right: String,
    mode: String,
  },
  emits: ["move", "showModal"],
  methods: {
    move(direction, index, element) {
      this.$emit("move", {
        direction: direction,
        index: index,
        element: element,
      });
    },
    showModal(columnName, index, element) {
      this.$emit("showModal", {
        columnName: columnName,
        index: index,
        element: element,
      });
    },
  },
};
</script>

<style>
.ghost {
  opacity: 0.3;
}
.lightTask {
  background-color: white;
}
.darkTask {
  background-color: rgb(58, 58, 58);
  color: white;
}
.controlBtn {
  cursor: pointer;
  width: 50px;
  height: 50px;
  border: 2px solid #1a99ff;
  border-radius: 10px;
  transition: background-color 0.5s ease-in-out;
}
.disabledBtn {
  border: 2px solid rgba(26, 153, 255, 0.4);
  cursor: default;
}
.disabledBtn img {
  opacity: 0.4;
}
.controls {
  display: flex;
  justify-content: space-between;
}
.taskCard {
  border: 2px solid #1a99ff;
  border-radius: 5px;
  padding: 20px;
  margin-bottom: 10px;
  transition: background-color 0.5s ease-in-out;
}
.headerTask {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.headerTask__title {
  margin: 0;
  font-size: 1.2rem;
}
</style>
