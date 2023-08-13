<template>
  <span v-if="value !== undefined">{{ filter(displayValue) }}</span>
</template>

<script>
import gsap from "gsap";

export default {
  name: "VNumberAnimation",
  props: {
    value: { type: Number, default: undefined },
    filter: { type: Function, default: (value) => value },
  },

  data() {
    return {
      displayValue: this.value,
      tweenValue: this.value,
    };
  },

  watch: {
    value: "valueWatcher",
  },

  methods: {
    valueWatcher(newValue) {
      if (newValue === undefined) {
        return;
      }

      gsap.to(this, {
        tweenValue: this.value,
        onUpdate: () => (this.displayValue = Math.ceil(this.tweenValue)),
      });
    },
  },
};
</script>
