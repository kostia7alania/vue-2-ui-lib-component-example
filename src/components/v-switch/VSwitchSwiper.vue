<template>
  <div :class="$style.TabsSwiper">
    <!-- swiper -->
    <div ref="sliderRef" :class="$style.swiper" class="swiper">
      <!-- pass all props -->
      <VSwitch
        v-bind="$attrs"
        v-on="$listeners"
        in-swiper
        class="swiper-wrapper"
      />

      <div :class="$style.nav">
        <button
          ref="prev"
          :class="$style.navPrev"
          :disabled="isBeginning"
          @click="slidePrev"
        >
          &lt;
        </button>

        <button
          ref="next"
          :class="$style.navNext"
          :disabled="isEnd"
          @click="slideNext"
        >
          &gt;
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import Swiper from "swiper";
import VSwitch from "./VSwitch.vue";

export default {
  name: "VSwitchSwiper",
  components: {
    VSwitch,
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
      window.t = this;
      return this.swiper?.isEnd;
    },
    isBeginning() {
      return this.swiper?.isBeginning;
    },
  },
  mounted() {
    this.$nextTick(() => {
      setTimeout(() => {
        this.initSlider();
      }, 1111);
    });
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
  border: 1px solid green;
  display: flex;
  width: 100%;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  .swiper {
    position: relative;
    // display: inline-block;
    width: 100%;
    .nav {
      position: absolute;
      top: 50%;

      right: 10px;
      left: 10px;

      z-index: 1;
      display: flex;
      align-items: center;
      justify-content: space-between;
      height: 0;

      .navPrev,
      .navNext {
        width: 24px;
        height: 24px;
        border: none;
        border-radius: 50%;
        box-shadow: none;
        background: rgba(40, 45, 60, 0.4);
        color: "blue";
        backdrop-filter: blur(8px);
        appearance: none;
        cursor: pointer;
        transition: 0.3s ease;
        user-select: none;

        &:disabled {
          opacity: 0;
          cursor: not-allowed;
        }
      }
    }
  }
}
</style>
