<template>
  <transition name="modal">
    <div v-if="show" class="modal-shadow" @click.self="closeModal">
      <div class="modal">
        <div class="modalcloseBtnContainter">
          <button class="modalcloseBtn" @click="closeModal">&#10006;</button>
        </div>
        <div class="taskInfContainer">
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
            <select v-model="newTask1.priority">
              <option selected disabled>выберите приоритет</option>
              <option>1</option>
              <option>2</option>
              <option>3</option>
            </select>
          </label>
          <button
            v-if="action == 'add'"
            class="addTaskBtn"
            v-on:click="sendBack(action)"
          >
            Сохранить
          </button>
          <button v-else class="addTaskBtn" v-on:click="sendBack(action)">
            Сохранить
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
  },
  emits: ["returned"],
  data: function () {
    return {
      show: false,
      newTask1: this.newTask,
    };
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
  background-color: rgba(0, 0, 0, 0.3);
  display: flex;
  justify-content: center;
  align-items: center;
}
.modal {
  width: 30%;
  height: 300px;
  background-color: white;
  padding: 30px 30px 10px 30px;
  border: 2px solid #1a99ff;
  border-radius: 5px;
}
.modalcloseBtnContainter {
  display: flex;
  justify-content: flex-end;
  margin: -20px -20px 0 0;
}
.modalcloseBtn {
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
.taskInfContainer,
.taskInfContainer label {
  display: flex;
  flex-direction: column;
}
.taskInfContainer {
  height: 100%;
  justify-content: space-around;
  color: #1a76c2;
  font-weight: 500;
}
.taskInfContainer label textarea,
.taskInfContainer label select {
  margin-top: 10px;
}

.modal-enter-active,
.modal-leave-active {
  transition: opacity 0.5s;
}

.modal-enter,
.modal-leave-to {
  opacity: 0;
}
.addTaskBtn {
  width: 100px;
  padding: 10px;
  margin: 0 auto;
  border: none;
  background-color: #219afb;
  color: white;
  cursor: pointer;
}
.addTaskBtn:hover {
  background-color: #218fe9;
}
</style>
