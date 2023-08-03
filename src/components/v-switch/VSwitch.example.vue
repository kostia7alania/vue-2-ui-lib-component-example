<template>
  <div :class="$style.VSwitchExample">
    <div :class="$style.settings">
      <!-- SIZES -->
      <fieldset>
        <legend>Sizes:</legend>

        <div
          v-for="sizeItem in sizes"
          :key="sizeItem.value"
          :class="$style.settingsItem"
        >
          <label @mouseover="size = sizeItem.value">
            <input
              type="radio"
              :name="sizeItem.value"
              :value="sizeItem.value"
              :checked="sizeItem.value === size"
              @change="size = sizeItem.value"
            />
            {{ sizeItem.label }}</label
          >
        </div>
      </fieldset>

      <!-- Purposes -->
      <fieldset>
        <legend>Purposes:</legend>

        <div
          v-for="purposeItem in purposes"
          :key="purposeItem.value"
          :class="$style.settingsItem"
        >
          <label @mouseover="purpose = purposeItem.value">
            <input
              type="radio"
              :name="purposeItem.value"
              :value="purposeItem.value"
              :checked="purposeItem.value === purpose"
              @change="purpose = purposeItem.value"
            />
            {{ purposeItem.label }}</label
          >
        </div>
      </fieldset>

      <!-- Colored -->
      <fieldset>
        <legend>Colored:</legend>

        <div
          v-for="coloredItem in coloreds"
          :key="coloredItem.value"
          :class="$style.settingsItem"
        >
          <label @mouseover="colored = coloredItem.value">
            <input
              type="radio"
              :value="coloredItem.value"
              :checked="coloredItem.value === colored"
              @change="colored = coloredItem.value"
            />
            {{ coloredItem.label }}
          </label>
        </div>
      </fieldset>

      <!-- Disableds -->
      <fieldset>
        <legend>Disabled:</legend>

        <div
          v-for="item in disableds"
          :key="item.value"
          :class="$style.settingsItem"
        >
          <label @mouseover="disabled = item.value">
            <input
              type="radio"
              :value="item.value"
              :checked="item.value === disabled"
              @change="disabled = item.value"
            />
            {{ item.label }}
          </label>
        </div>
      </fieldset>
    </div>

    <!-- EXAMPLE 1 -->

    <h1>VSwitch</h1>

    <VSwitch
      v-model="model"
      :class="$style.VSwitchScroll"
      :items="items"
      :size="size"
      :purpose="purpose"
      :colored="colored"
      :disabled="disabled"
    />

    <!-- EXAMPLE 2 -->

    <h1>VSwitchSwiper</h1>

    <div :class="$style.VSwitchSwipe">
      <VSwitchSwiper
        v-model="model"
        :items="items"
        :size="size"
        :purpose="purpose"
        :colored="colored"
        :disabled="disabled"
      />
    </div>
  </div>
</template>

<script>
import VSwitch from "./VSwitch.vue";
import VSwitchSwiper from "./VSwitchSwiper.vue";
import {
  VSwitchPurposeMap,
  VSwitchSizeMap,
  VSwitchColoredMap,
  VSwitchDefaults,
} from "./VSwitch.types.js";

const items = Array(33)
  .fill()
  .map((_, value) => ({ label: `Test ${value}`, value }));

const sizes = [
  { label: "Small", value: VSwitchSizeMap.s },
  { label: "Medium", value: VSwitchSizeMap.m },
  { label: "Large", value: VSwitchSizeMap.l },
];

const purposes = [
  { label: "Primary", value: VSwitchPurposeMap.primary },
  { label: "Secondary", value: VSwitchPurposeMap.secondary },
];
const coloreds = [
  { label: "On", value: VSwitchColoredMap.true },
  { label: "Off", value: VSwitchColoredMap.false },
];
const disableds = [
  { label: "True", value: true },
  { label: "False", value: false },
];

export default {
  data() {
    return {
      model: undefined,

      items,
      sizes,
      purposes,
      coloreds,
      disableds,
      size: VSwitchDefaults.size,
      purpose: VSwitchDefaults.purpose,
      colored: VSwitchDefaults.colored,
      disabled: false,
    };
  },
  components: {
    VSwitch,
    VSwitchSwiper,
  },
};
</script>

<style lang="scss" module>
.VSwitchExample {
  background-color: #f0f0f0;
  padding: 24px;
  .settings {
    display: flex;
    justify-content: center;
    gap: 32px;
    margin-bottom: 24px;

    .settingsItem {
      text-align: start;
      input,
      label {
        cursor: pointer;
      }
    }
  }

  .VSwitchScroll {
    overflow: auto;
    padding: 10px;
    width: 100%;
  }

  .VSwitchSwipe {
    padding: 64px;
    background-color: #bbbfff;
    border-radius: 10px;
    max-width: 777px;
    margin: auto;
  }
}
</style>
