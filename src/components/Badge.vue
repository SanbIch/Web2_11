<template>
  <div class="task-card-header__priority-sign">
    <slot></slot>
  </div>
</template>

<style>
.task-card-header__priority-sign {
  width: 20px;
  height: 20px;
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 50%;
  border: 2px solid #1a99ff;
  color: black;
}
</style>
