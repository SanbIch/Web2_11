<template>
  <transition name="modal">
    <div v-if="show" class="modal-shadow" @click.self="closeModal">
      <div
        class="modal-window"
        :class="mode == 'light' ? 'modal-window_light' : 'modal-window_dark'"
      >
        <div class="close-btn-containter">
          <button class="close-btn-containter__close-btn" @click="closeModal">
            &#10006;
          </button>
        </div>
        <div
          class="task-info-container"
          :class="
            mode == 'light'
              ? 'task-info-container_light'
              : 'task-info-container_dark'
          "
        >
          <label for="">
            Описание
            <textarea
              name=""
              id=""
              cols="30"
              rows="10"
              placeholder="Описание"
              v-model="newTask1.desc"
              required
            ></textarea>
          </label>
          <label for="">
            Приоритет
            <select v-model="newTask1.priority" required>
              <option disabled>выберите приоритет</option>
              <option>1</option>
              <option>2</option>
              <option>3</option>
            </select>
          </label>
          <button
            class="task-info-container__add-task-btn"
            :class="
              disabledBtn == 1
                ? 'task-info-container__add-task-btn_disabled'
                : 'task-info-container__add-task-btn_active'
            "
            v-on:click="sendBack(action)"
            type="submit"
            :disabled="disabledBtn"
          >
            {{ btnText }}
          </button>
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  name: "ModalWindow",
  props: {
    columns: Object,
    action: String,
    newTask: Object,
    mode: String,
  },
  emits: ["returned"],
  data: function () {
    return {
      show: false,
      newTask1: this.newTask,
    };
  },
  computed: {
    btnText: function () {
      if (this.action == "add") return "Создать";
      else return "Сохранить";
    },
    disabledBtn: function () {
      if (
        this.newTask1.desc == null ||
        this.newTask1.priority == "выберите приоритет"
      )
        return 1;
      else return 0;
    },
  },
  mounted() {
    document.body.addEventListener("keyup", (e) => {
      if (e.code == "Escape") {
        this.closeModal(); // how to hide any open modal?
      }
    });
  },
  methods: {
    closeModal: function () {
      this.show = false;
    },
    sendBack(action) {
      this.$emit("returned", {
        desc: this.newTask1.desc,
        date: this.makeCalculate(),
        priority: this.newTask1.priority,
        action: action,
        columnName: this.newTask1.columnName,
        index: this.newTask1.index,
      });
      this.newTask1.desc = "";
      this.newTask1.priority = "";
      this.closeModal();
    },
    makeCalculate() {
      let now = new Date();
      let day = now.getDate();
      let month = now.getMonth() + 1;
      let year = now.getFullYear();
      let hours = now.getHours();
      let minutes = now.getMinutes();
      let seconds = now.getSeconds();
      return (
        day +
        "." +
        month +
        "." +
        year +
        " " +
        hours +
        ":" +
        minutes +
        ":" +
        seconds
      );
    },
  },
};
</script>

<style>
.modal-shadow {
  position: absolute;
  top: 0px;
  right: 0px;
  bottom: 0px;
  left: 0px;
  width: 100%;
  height: 100vh;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}
.modal-window {
  width: 30%;
  height: 300px;
  padding: 30px 30px 10px 30px;
  border: 2px solid #1a99ff;
  border-radius: 5px;
}
.modal-window_light {
  background-color: white;
}
.modal-window_dark {
  background-color: rgb(97, 97, 97);
}
.close-btn-containter {
  display: flex;
  justify-content: flex-end;
  margin: -20px -20px 0 0;
}
.close-btn-containter__close-btn {
  width: 25px;
  height: 25px;
  border: 2px solid #1a99ff;
  color: #1a99ff;
  border-radius: 50%;
  cursor: pointer;
  display: flex;
  justify-content: center;
  align-items: center;
}
.task-info-container,
.task-info-container label {
  display: flex;
  flex-direction: column;
}
.task-info-container {
  height: 100%;
  justify-content: space-around;
  font-weight: 500;
}
.task-info-container_light {
  color: #1a76c2;
}
.task-info-container_dark {
  color: white;
}
.task-info-container label textarea,
.task-info-container label select {
  margin-top: 10px;
}
.task-info-container_dark label textarea,
.task-info-container_dark label select {
  background-color: rgb(70, 70, 70);
  color: white;
}
.task-info-container_dark label textarea::placeholder {
  color: rgba(255, 255, 255, 0.5);
}
.modal-enter-active,
.modal-leave-active {
  transition: opacity 0.5s;
}

.modal-enter,
.modal-leave-to {
  opacity: 0;
}
.task-info-container__add-task-btn {
  width: 100px;
  padding: 10px;
  margin: 0 auto;
  border: none;
  background-color: #219afb;
  color: white;
  cursor: pointer;
}
.task-info-container__add-task-btn_disabled {
  opacity: 0.5;
  cursor: default;
}
.task-info-container__add-task-btn_active:hover {
  background-color: #218fe9;
}
</style>
