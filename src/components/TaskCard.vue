<template>
  <draggable :list="tasks" group="tasks" itemKey="name" ghost-class="ghost">
    <template #item="{ element, index }">
      <div
        class="task-card"
        :class="mode == 'light' ? 'task-card_light' : 'task-card_dark'"
      >
        <div class="task-card-header">
          <h3 class="task-card-header__title">Задача №{{ element.id }}</h3>
          <badge
            :class="[
              element.priority == 1
                ? 'task-card-header__priority-sign_first-priority'
                : '',
              element.priority == 2
                ? 'task-card-header__priority-sign_second-priority'
                : '',
              element.priority == 3
                ? 'task-card-header__priority-sign_third-priority'
                : '',
            ]"
            >{{ element.priority }}</badge
          >
        </div>
        <div class="task-card__description-task">
          <p>{{ element.desc }}</p>
          <span>{{ element.date }}</span>
        </div>
        <div class="task-card-controls">
          <button
            :disabled="columnName == 'plan'"
            :class="[
              columnName == 'plan'
                ? 'task-card-controls__control-btn_disabled'
                : '',
              mode == 'light'
                ? 'task-card-controls__control-btn_light'
                : 'task-card-controls__control-btn_dark',
            ]"
            class="task-card-controls__control-btn"
            @click="move(left, index, element)"
          >
            <img src="../assets/left-arrow.svg" alt="" />
          </button>
          <button
            class="task-card-controls__control-btn"
            :class="
              mode == 'light'
                ? 'task-card-controls__control-btn_light'
                : 'task-card-controls__control-btn_dark'
            "
            @click="showModal(columnName, index, element)"
          >
            Edit
          </button>
          <button
            class="task-card-controls__control-btn"
            :class="
              mode == 'light'
                ? 'task-card-controls__control-btn_light'
                : 'task-card-controls__control-btn_dark'
            "
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
.task-card {
  border: 2px solid #1a99ff;
  border-radius: 5px;
  padding: 20px;
  margin-bottom: 10px;
  transition: background-color 0.5s ease-in-out;
}
.task-card_light,
.task-card-controls__control-btn_light {
  background-color: white;
}
.task-card_dark,
.task-card-controls__control-btn_dark {
  background-color: rgb(58, 58, 58);
  color: white;
}
.task-card-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.task-card-header__title {
  margin: 0;
  font-size: 1.2rem;
}
.task-card-header__priority-sign_first-priority {
  background-color: #ffa4a4;
}
.task-card-header__priority-sign_second-priority {
  background-color: #fffc9f;
}
.task-card-header__priority-sign_third-priority {
  background-color: #adedc9;
}
.task-card-controls {
  display: flex;
  justify-content: space-between;
}
.task-card-controls__control-btn {
  cursor: pointer;
  width: 50px;
  height: 50px;
  border: 2px solid #1a99ff;
  border-radius: 10px;
  transition: background-color 0.5s ease-in-out;
}
.task-card-controls__control-btn_disabled {
  border: 2px solid rgba(26, 153, 255, 0.4);
  cursor: default;
}
.task-card-controls__control-btn_disabled img {
  opacity: 1;
}
</style>
