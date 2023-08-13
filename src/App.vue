<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <VSwitchExample />
    <VNumberAnimationExample />
  </div>
</template>

<script>
import VSwitchExample from "@/components/v-switch/VSwitch.example.vue";
import VNumberAnimationExample from "@/components/v-number-animation/VNumberAnimation.example.vue";

export default {
  name: "App",
  components: {
    VSwitchExample,
    VNumberAnimationExample,
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
