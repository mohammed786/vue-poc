<template>
  <Generator :id="id" />
  <button @click="id++">Add Row</button>
</template>

<script>
import Generator from "./components/Generator.vue";
export default {
  name: "App",
  components: {
    Generator,
  },
  data() {
    return {
      id: 1,
    };
  },
};
</script>

<style lang="scss">
html,
body {
  margin: 0;
  height: 100%;
  background: #f9f9f9;
}
.container {
  padding-top: 20px;
}
</style>
