<template>
  <div>
    <div>valueFixedLength => {{ valueFixedLength }}</div>
    <div>displayValue => {{ displayValue }}</div>
    <span v-if="value !== undefined">{{ filterMethod(displayValue) }}</span>
  </div>
</template>

<script>
import gsap from "gsap";

export default {
  name: "VNumberAnimation",
  props: {
    value: { type: [Number, String], default: undefined },
    filterMethod: { type: Function, default: (value) => value },
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
  computed: {
    isValueInteger() {
      return Number.isInteger(this.value);
    },
    valueFixedLength() {
      if (this.isValueInteger || !this.value) {
        return 0;
      }

      return String(this.value).split(".").slice(-1)?.[0].length;
    },
  },
  methods: {
    valueWatcher(newValue) {
      if (newValue === undefined) {
        return;
      }

      gsap.to(this, {
        tweenValue: this.value,
        onUpdate: () => {
          this.displayValue = Number(this.tweenValue).toFixed(
            this.valueFixedLength
          );
        },
      });
    },
  },
};
</script>
