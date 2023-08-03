<template>
  <button
    :disabled="disabled"
    :class="[
      $style.VSwitchTab,
      {
        'r-l5-class': size === VSwitchSizeMap.s,
        'r-l4-class': size === VSwitchSizeMap.m,
        'r-l3-class': size === VSwitchSizeMap.l,
        // size
        [$style.small]: size === VSwitchSizeMap.s,
        [$style.medium]: size === VSwitchSizeMap.m,
        [$style.large]: size === VSwitchSizeMap.l,
        // purpose
        [$style.primary]: purpose === VSwitchPurposeMap.primary,
        [$style.secondary]: purpose === VSwitchPurposeMap.secondary,
        // state
        [$style.selected]: selected,
        [$style.colored]: colored,
        [$style.disabled]: disabled,
      },
    ]"
    @click="$emit('click')"
  >
    {{ label }}
  </button>
</template>

<script>
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
    selected: {
      // State = Active (in Figma)
      type: Boolean,
      default: false,
    },

    // props from figma
    label: { type: String, default: undefined },
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
  data() {
    return {
      VSwitchPurposeMap,
      VSwitchSizeMap,
    };
  },
};
</script>

<style module lang="scss">
@import "@/assets/variables.scss";
@import "@/assets/r-text.scss";

.VSwitchTab {
  border-radius: 6px;
  font-weight: 500;
  white-space: nowrap;
  transition: 0.2s ease;

  // size
  &.small {
    height: 28px;
    padding: 0 12px;
  }
  &.medium {
    height: 32px;
    padding: 0 16px;
  }
  &.large {
    height: 40px;
    padding: 0 20px;
  }
  &:not(:disabled) {
    &:not(.selected) {
      cursor: pointer;
    }

    // purpose
    &.primary:not(:disabled) {
      &:hover:not(.selected) {
        background-color: $r-base-cloud;
        &.colored {
          background-color: $r-base-wind;
        }
      }

      &.selected {
        background-color: $r-primary-sky;
        color: $r-base-cloud;
      }
    }

    &.secondary:not(:disabled) {
      color: $r-base-500;

      &:hover:not(.selected) {
        background-color: $base-cloud;
      }

      &.colored {
        color: $r-base-500;
        background-color: transparent;

        &:hover:not(.selected) {
          background-color: $r-base-wind;
        }
      }

      &.selected {
        color: $r-primary-sky;
        background-color: $r-base-cloud;

        &.colored {
          background-color: $r-base-wind;
          color: $r-primary-sky;
        }
      }
    }
  }
  &.disabled {
    color: $r-base-400;
  }
}
</style>

<style lang="scss">
@import "@/assets/variables.scss";
@import "@/assets/r-text.scss";
</style>
