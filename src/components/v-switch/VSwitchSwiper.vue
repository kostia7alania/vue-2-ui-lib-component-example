<template>
  <div :class="$style.TabsSwiper">
    <!-- swiper -->
    <div ref="sliderRef" :class="$style.swiper" class="swiper">
      <!-- pass all props -->
      <VSwitch
        v-bind="$attrs"
        v-on="$listeners"
        class="swiper-wrapper"
        in-swiper
      />
    </div>

    <div :class="$style.nav">
      <VButton
        ref="prev"
        color="white"
        round
        :class="[
          $style.navNext,
          {
            [$style.disabled]: isBeginning,
          },
        ]"
        :disabled="isBeginning"
        @click="slidePrev"
      >
        &lt;
      </VButton>

      <VButton
        ref="next"
        color="white"
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
    </div>
  </div>
</template>

<script>
import Swiper from "swiper";
import VSwitch from "./VSwitch.vue";
import VButton from "@/components/v-button/VButton.vue";

export default {
  name: "VSwitchSwiper",
  components: {
    VSwitch,
    VButton,
  },
  // props: see in VSwitch
  inheritAttrs: false,
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
        mousewheel: {
          forceToAxis: true,
          sensitivity: 4,
          releaseOnEdges: true,
        },
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
.TabsSwiper {
  width: 100%;
  position: relative;

  .swiper {
    overflow: hidden;
    width: 100%;
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

    .navPrev,
    .navNext {
      cursor: pointer;
      transition: 0.3s ease;
      user-select: none;

      &.disabled {
        opacity: 0;
        cursor: not-allowed;
      }
    }
  }
}
</style>
