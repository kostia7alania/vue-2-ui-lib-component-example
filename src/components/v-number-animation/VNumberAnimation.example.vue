<template>
  <div>
    <h1>VNumberAnimation</h1>
    <div>
      <input type="text" v-model.number="model1" />
      <VNumberAnimation :value="model1" />
    </div>
    <div>
      <input type="text" v-model.number="model2" />
      <VNumberAnimation :value="model2" :filter-method="splitComma" />
    </div>
  </div>
</template>

<script>
import VNumberAnimation from "@/components/v-number-animation/VNumberAnimation.vue";

const splitComma = (num) => {
  if (typeof num !== "number" && !Number.isNaN(num)) {
    console.warn('[Utils/splitComma] Аргумент "num" должен быть Number: ', num);
    return "";
  }
  return num.toString().replace(".", ",");
  //   return num.toLocaleString("ru-RU");
};

export default {
  components: {
    VNumberAnimation,
  },
  data() {
    return {
      model1: 12345,
      model2: undefined,

      splitComma,
    };
  },
};
</script>
