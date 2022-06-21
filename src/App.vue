<template>
  <header>
    <ComponentHeader />
  </header>

  <main>
    <ComponentMain />
  </main>
</template>

<script>
import ComponentHeader from "./components/Header/ComponentHeader.vue";
import ComponentMain from "./components/Main/ComponentMain.vue";

export default {
  name: "App",
  components: {
    ComponentHeader,
    ComponentMain,
  },
};
</script>

<style>
</style>
