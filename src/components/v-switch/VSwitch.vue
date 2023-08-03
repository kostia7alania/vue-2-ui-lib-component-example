<template>
  <div
    :class="[
      $style.VSwitch,
      {
        [$style.colored]: colored,
      },
    ]"
  >
    <VSwitchTab
      v-for="(item, index) in items"
      :class="{
        'swiper-slide': inSwiper,
      }"
      :selected="value === item.value"
      :label="item.label"
      :key="index + String(item.label)"
      :size="size"
      :purpose="purpose"
      :colored="colored"
      :disabled="disabled"
      @click="$emit('input', item.value)"
    />
  </div>
</template>

<script>
import VSwitchTab from "./VSwitchTab.vue";
import {
  VSwitchPurposeMap,
  VSwitchSizeMap,
  VSwitchColoredMap,
  VSwitchDefaults,
} from "./VSwitch.types.js";

export default {
  props: {
    // native
    disabled: { type: Boolean, default: false },
    // custom
    value: {
      type: [String, Number],
      default: undefined,
    },
    items: { type: Array, default: () => [] },
    inSwiper: { type: Boolean, default: false },
    // props from figma
    purpose: {
      type: String,
      default: VSwitchDefaults.purpose,
      validator: (val) => val in VSwitchPurposeMap,
    },
    size: {
      type: String,
      default: VSwitchDefaults.size,
      validator: (val) => val in VSwitchSizeMap,
    },
    colored: {
      type: Boolean,
      default: VSwitchDefaults.colored,
      validator: (val) => val in VSwitchColoredMap,
    },
  },
  components: {
    VSwitchTab,
  },
};
</script>

<style lang="scss" module>
@import "@/assets/variables.scss";
@import "@/assets/r-text.scss";

.VSwitch {
  display: inline-flex;
  gap: 4px;
  border-radius: 8px;
  background-color: $r-base-wind;
  &.colored {
    background-color: $r-base-cloud;
  }
}
</style>

<style lang="scss">
@import "@/assets/variables.scss";
@import "@/assets/r-text.scss";
</style>
