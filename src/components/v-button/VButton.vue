<template>
  <!-- Стандартная кнопка -->
  <component
    :is="tag"
    :class="[$style.VButton, classList]"
    @click="$emit('click', $event)"
  >
    <slot>
      {{ text }}
    </slot>
  </component>
</template>

<script>
/**
 * THIS COMPONENTS COPY-PASTED HERE FROM PRODUCTION PROJECT ONLY FOR VSwitchSwipe.vue-component
 */

export default {
  name: "VButton",

  props: {
    text: {
      type: String,
      default: "",
    },

    tag: {
      type: String,
      default: "button",
      validator: (val) => ["button", "a", "span", "div"].includes(val),
    },

    fill: {
      type: Boolean,
      default: false,
    },

    size: {
      type: String,
      default: "m",
      validator: (val) => ["l", "m", "s", "xs", "custom"].includes(val),
    },

    color: {
      type: String,
      default: "blue",
      validator: (val) =>
        ["blue", "white", "gray", "grey", "yellow"].includes(val),
    },

    round: {
      type: Boolean,
      default: false,
    },

    error: {
      type: Boolean,
      default: false,
    },

    noHover: {
      type: Boolean,
      default: false,
    },

    userSelect: {
      type: Boolean,
      default: false,
    },

    disabled: {
      type: Boolean,
      default: false,
    },

    noBorder: {
      type: Boolean,
      default: false,
    },
  },

  computed: {
    classList() {
      return {
        [this.$style["_fill"]]: this.fill,
        [this.$style[`_size-${this.size}`]]: this.size,
        [this.$style[`_${this.color}`]]: this.color,
        [this.$style["_error"]]: this.error,
        [this.$style["_round"]]: this.round,
        [this.$style["_no-hover"]]: this.noHover,
        [this.$style["_user-select"]]: this.userSelect,
        [this.$style["_disabled"]]: this.disabled,
        [this.$style["_no-border"]]: this.noBorder,
      };
    },
  },
};
</script>

<style lang="scss" module>
@import "@/assets/variables.scss";
@import "@/assets/r-text.scss";

@import "@/assets/mixins.scss";

.VButton {
  position: relative;
  -webkit-appearance: none;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  height: 56px;
  padding: 0 40px;
  font-size: 16px;
  line-height: 16px;
  font-weight: 500;
  letter-spacing: -0.01em;
  border: none;
  border-radius: 28px;
  transition: 0.3s;
  overflow: hidden;
  outline: none;
  cursor: pointer;
  user-select: none;
  -webkit-mask-image: -webkit-radial-gradient(white, black);

  &:after {
    content: "";
    position: absolute;
    top: 50%;
    left: 50%;
    width: 100px;
    height: 100px;
    border-radius: 50%;
    transform: translate(-50%, -50%) scale(0);
    transition: 0.3s;
    background-color: rgba(#fff, 0.2);
    pointer-events: none;
    z-index: -1;
  }

  // размеры
  &._size-l {
    @include respond-to(mobile) {
      height: 48px;
      padding: 0 28px;
      font-size: 14px;
      line-height: 14px;
    }
  }

  &._size-m {
    padding: 0 32px;
    height: 48px;
    font-size: 14px;
    line-height: 14px;
    border-radius: 24px;

    @include respond-to(mobile) {
      height: 40px;
      padding: 0 20px;
      font-size: 14px;
      line-height: 14px;
    }
  }

  &._size-s {
    padding: 0 24px;
    height: 40px;
    border-radius: 20px;
    font-size: 14px;
    line-height: 14px;

    @include respond-to(mobile) {
      height: 32px;
      padding: 0 20px;
      font-size: 12px;
      line-height: 12px;
    }
  }

  &._size-xs {
    padding: 0 24px;
    height: 32px;
    border-radius: 16px;
    font-size: 12px;
    line-height: 12px;
  }

  &._fill {
    flex: 1 1 auto;
  }

  &:not(._no-hover) {
    // должен стоять после размеров
    @include hover() {
      &:hover {
        border-radius: 8px;

        &:after {
          transform: translate(-50%, -50%) scale(6);
        }
      }
    }
  }

  &._user-select {
    user-select: all;
    cursor: unset;
  }

  // цвета
  &._white {
    background-color: $r-base-cloud;
    color: $r-primary-sky;
  }

  &._grey,
  &._gray {
    background-color: $r-base-wind;
    color: $r-primary-sky;

    &:after {
      background-color: $r-base-200;
    }

    &:active {
      &:after {
        background-color: $r-base-300;
      }
    }
  }

  &._blue {
    background-color: $r-primary-sky;
    color: #fff;

    &:active {
      &:after {
        background-color: $r-primary-300;
      }
    }
  }

  &._yellow {
    background-color: $r-option-sun;
    color: $r-base-stone;
  }

  &._error {
    background-color: $r-error-fire;
    color: #fff;

    @include hover() {
      &:hover {
        color: #fff;
      }
    }

    &:after {
      background-color: lighten($r-error-fire, 10%);
    }

    &:active {
      &:after {
        background-color: lighten($r-error-fire, 10%);
      }
    }
  }

  // круглая кнопка
  &._round {
    width: 56px;
    height: 56px;
    padding-left: 0;
    padding-right: 0;
    border-radius: 50%;

    &._size-m {
      width: 48px;
      height: 48px;
    }

    &._size-s {
      width: 40px;
      height: 40px;
    }

    &._size-xs {
      width: 32px;
      height: 32px;
    }
  }

  &._disabled {
    background-color: $r-base-wind;
    color: $r-base-500;
    cursor: not-allowed;
    pointer-events: none;

    &:after {
      background-color: $r-base-200;
    }

    &:active {
      &:after {
        background-color: $r-base-300;
      }
    }
  }

  // static borders
  &._no-border {
    border-radius: 4px;

    @include hover() {
      &:hover {
        border-radius: 4px;
      }
    }
  }
}
</style>
