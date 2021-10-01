<template>
  <header class="header">
    <img src="../assets/headerLogo.svg" alt="logo" class="header__logo" />
    <h1 class="header__project-name">Название проекта</h1>
    <div class="header__toggle-btn">
      <p>{{ mode == "dark" ? "Темная тема" : "Светлая тема" }}</p>
      <Toggle :mode="mode" @toggle="$emit('toggle')" />
    </div>
  </header>
</template>

<script>
import Toggle from "@/components/Toggle";

export default {
  props: ["mode"],
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
.header {
  background-color: #2699fb;
  color: white;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  padding: 0 10%;
}
.header__logo {
  width: 40px;
}
.header__project-name {
  font-size: 1.5rem;
  font-weight: 400;
}
.header__toggle-btn {
  display: flex;
  align-items: center;
}
</style>
