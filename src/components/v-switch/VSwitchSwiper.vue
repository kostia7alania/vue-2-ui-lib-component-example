<template>
  <div :class="$style.TabsSwiper">
    <!-- swiper -->
    <div ref="sliderRef" :class="$style.swiper" class="swiper">
      <!-- pass all props -->
      <VSwitch v-bind="$attrs" v-on="$listeners" in-swiper />
    </div>

    <div :class="$style.nav">
      <!------
        MOBILE
       ------->
      <template v-if="isMobile">
        <!-- prev -->
        <VSwitchTab
          ref="prev"
          v-bind="$attrs"
          :class="[
            $style.navPrev,
            {
              [$style.disabled]: isEnd,
            },
          ]"
          @click="slideNext"
        >
          &gt;
        </VSwitchTab>

        <!-- next -->
        <VSwitchTab
          ref="next"
          v-bind="$attrs"
          :class="[
            $style.navNext,
            {
              [$style.disabled]: isBeginning,
            },
          ]"
          @click="slidePrev"
        >
          &lt;
        </VSwitchTab>
      </template>

      <!-----
        DESKTOP
       ------>
      <template v-else>
        <!-- prev -->
        <VButton
          ref="prev"
          color="white"
          size="xs"
          round
          :class="[
            $style.navPrev,
            {
              [$style.disabled]: isBeginning,
            },
          ]"
          :disabled="isBeginning"
          @click="slidePrev"
        >
          &lt;
        </VButton>

        <!-- next -->
        <VButton
          ref="next"
          color="white"
          size="xs"
          round
          :disabled="isEnd"
          :class="[
            $style.navNext,
            {
              [$style.disabled]: isEnd,
            },
          ]"
          @click="slideNext"
        >
          &gt;
        </VButton>
      </template>
    </div>
  </div>
</template>

<script>
import Swiper from "swiper";
import VSwitch from "./VSwitch.vue";
import VButton from "@/components/v-button/VButton.vue";
import VSwitchTab from "./VSwitchTab.vue";

export default {
  name: "VSwitchSwiper",
  components: {
    VSwitch,
    VButton,
    VSwitchTab,
  },
  // props: see in VSwitch
  inheritAttrs: false,
  props: {
    // TODO: use local util
    isMobile: Boolean,
  },
  data() {
    return {
      swiper: null,
    };
  },

  beforeDestroy() {
    if (this.swiper) {
      this.swiper.destroy();
    }
  },
  computed: {
    isEnd() {
      return this.swiper?.isEnd;
    },
    isBeginning() {
      return this.swiper?.isBeginning;
    },
  },
  mounted() {
    this.initSlider();
  },

  methods: {
    slideNext() {
      this.swiper.slideNext();
    },
    slidePrev() {
      this.swiper.slidePrev();
    },
    initSlider() {
      this.swiper = new Swiper(this.$refs.sliderRef, {
        observer: true,
        observeParents: true,
        slidesPerView: "auto",
        speed: 1000,
        // centeredSlides: false,
        spaceBetween: 4,
        loop: 0,
        allowTouchMove: true,
        freeMode: true,
        // mousewheel: {
        //   forceToAxis: true,
        //   sensitivity: 4,
        //   releaseOnEdges: true,
        // },
        navigation: {
          nextEl: this.$refs.next?.$el || this.$refs.next,
          prevEl: this.$refs.prev?.$el || this.$refs.prev,
          disabledClass: "_disabled",
        },
      });
    },
  },
};
</script>

<style lang="scss" module>
@import "@/assets/variables.scss";
@import "@/assets/mixins.scss";

.TabsSwiper {
  width: 100%;
  position: relative;

  .swiper {
    border-radius: 8px;
    background-color: $r-base-wind;

    overflow: hidden;
    width: 100%;

    @include respond-to(mobile) {
      padding: 0;
    }
  }

  .nav {
    position: absolute;
    top: 50%;

    right: -16px;
    left: -16px;

    z-index: 1;
    display: flex;
    align-items: center;
    justify-content: space-between;
    height: 0;

    @include respond-to(mobile) {
      right: 4px;
      left: 4px;
    }

    .navPrev,
    .navNext {
      cursor: pointer;
      transition: 0.3s ease;
      user-select: none;

      &.disabled {
        opacity: 0;
        cursor: not-allowed;
      }

      @include respond-to(mobile) {
        padding: 0;
        aspect-ratio: 1/1;
        background-color: $r-base-wind; // hardcode
      }
    }
    .navPrev.disabled {
      transform: scale(0);
    }
    .navNext.disabled {
      transform: scale(0);
    }
  }
}
</style>
