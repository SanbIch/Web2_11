<template>
  <div class="prioritySign">
    <slot></slot>
  </div>
</template>

<style>
.prioritySign {
  width: 20px;
  height: 20px;
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 50%;
  border: 2px solid #1a99ff;
}
.firstPriority {
  background-color: #ffa4a4;
}
.secondPriority {
  background-color: #fffc9f;
}
.thirdPriority {
  background-color: #adedc9;
}
</style>
