<template>
  <header>
    <img src="../assets/headerLogo.svg" alt="logo" class="logo" />
    <h1 class="headerText">Название проекта</h1>
    <div class="toggleBtn">
      <p>{{ mode == "dark" ? "Теманая тема" : "Светлая тема" }}</p>
      <Toggle :mode="mode" @toggle="$emit('toggle')" />
    </div>
  </header>
</template>

<script>
import Toggle from "@/components/Toggle";

export default {
  components: {
    Toggle,
  },
  data() {
    return {
      value: true,
    };
  },
};
</script>

<style>
header {
  background-color: #2699fb;
  color: white;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  padding: 0 10%;
}
.headerText {
  font-size: 1.5rem;
  font-weight: 400;
}
.logo {
  width: 40px;
}
.toggleBtn {
  display: flex;
  align-items: center;
}
</style>
