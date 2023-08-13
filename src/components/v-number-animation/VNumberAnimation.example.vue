<template>
  <div>
    <h1>VNumberAnimation</h1>
    <div>
      <input type="text" v-model="model1" />
      <VNumberAnimation :value="model1" />
    </div>
    <div>
      <input type="text" v-model="model2" />
      <VNumberAnimation v-model="model2" />
    </div>
  </div>
</template>

<script>
import VNumberAnimation from "@/components/v-number-animation/VNumberAnimation.vue";

export default {
  components: {
    VNumberAnimation,
  },
  data() {
    return {
      model1: 12345,
      model2: undefined,
    };
  },
};
</script>
