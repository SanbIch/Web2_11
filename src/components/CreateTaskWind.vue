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
            <textarea name="" id="" cols="30" rows="10"></textarea>
          </label>
          <label for="">
            Приоритет
            <select>
              <option selected disabled>выберите приоритет</option>
              <option>1</option>
              <option>2</option>
              <option>3</option>
            </select>
          </label>
          <button>Сохранить</button>
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  name: "ModalWindow",
  data: function () {
    return {
      show: false,
    };
  },
  methods: {
    closeModal: function () {
      this.show = false;
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
  padding: 40px;
  border: 2px solid #1a99ff;
  border-radius: 5px;
}
.modalcloseBtnContainter {
  display: flex;
  justify-content: flex-end;
  margin: -30px -30px 0 0;
}
.taskInfContainer,
.taskInfContainer label {
  display: flex;
  flex-direction: column;
}
.taskInfContainer {
  height: 100%;
  justify-content: space-around;
}

.modal-enter-active,
.modal-leave-active {
  transition: opacity 0.5s;
}

.modal-enter,
.modal-leave-to {
  opacity: 0;
}
</style>
