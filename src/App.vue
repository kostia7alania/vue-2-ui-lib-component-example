<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <VSwitchExample />
  </div>
</template>

<script>
import VSwitchExample from "./components/v-switch/VSwitch.example.vue";

export default {
  name: "App",
  components: {
    VSwitchExample,
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

button {
  all: unset;
}
</style>
