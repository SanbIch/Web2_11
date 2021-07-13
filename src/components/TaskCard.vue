<template>
  <draggable :list="column.tasks" itemKey="name">
    <template #item="{ element }">
      <div>{{ element.date }}</div>
      <!-- <div class="taskCard">
        <div class="headerTask">
          <h3 class="headerTask__title">Задача №{{ element.id }}</h3>
          <badge
            :class="[
              task.priority == 1 ? 'firstPriority' : '',
              task.priority == 2 ? 'secondPriority' : '',
              task.priority == 3 ? 'thirdPriority' : '',
            ]"
            >{{ task.priority }}</badge
          >
        </div>
        <div class="descriptionTask">
          <p>Lorem sdn vasdjnk vsjdv sjldv sdjv dsv dsjv</p>
          <span>{{ task.date }}</span>
        </div>
        <div class="controls">
          <button class="controlBtn left">
            <img src="../assets/left-arrow.svg" alt="" />
          </button>
          <button class="controlBtn edit">Edit</button>
          <button class="controlBtn right">
            <img src="../assets/right-arrow.svg" alt="" />
          </button>
        </div>
      </div> -->
    </template>
  </draggable>
</template>

<script>
// import Badge from "./Badge.vue";
import draggable from "vuedraggable";
export default {
  components: {
    draggable,
    // Badge,
  },
  props: {
    task: {
      type: Object,
      default: () => ({}),
    },
  },
  computed: {
    badgeColor() {
      const mappings = {
        Design: "purple",
        "Feature Request": "teal",
        Backend: "blue",
        QA: "green",
        default: "teal",
      };
      return mappings[this.task.type] || mappings.default;
    },
  },
};
</script>

<style>
.controlBtn {
  cursor: pointer;
  width: 50px;
  height: 50px;
  border: 2px solid #1a99ff;
  background-color: white;
  border-radius: 10px;
}
.controls {
  display: flex;
  justify-content: space-between;
}
.taskCard {
  background-color: white;
  border: 2px solid #1a99ff;
  border-radius: 5px;
  padding: 20px;
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
