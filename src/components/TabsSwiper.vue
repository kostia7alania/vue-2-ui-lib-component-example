<template>
  <div :class="$style.TabsSwiper">
    begin:{{ isBeginning }} | end: {{ isEnd }}
    <!-- swiper -->
    <div ref="sliderRef" :class="$style.swiper">
      <div :class="$style.wrapper" class="swiper-wrapper">
        <div
          v-for="(image, index) in gallery"
          :key="index"
          class="swiper-slide"
        >
          {{ image }}
        </div>
      </div>

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

const gallery = [
  "Все",
  "Самолет",
  "Семейная",
  "Военная",
  "разззззз",
  "двааааааааааа",
  "триииииииии",
];

export default {
  name: "AboutSlider",

  data() {
    return {
      gallery,
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
      }, 111);
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
        slidesPerView: "auto",
        speed: 700,
        // centeredSlides: false,
        spaceBetween: 4,
        loop: false,
        allowTouchMove: true,
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
  max-width: 300px;
  border: 1px solid green;
  overflow: hidden;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin: auto;
  // padding: 0 10px;

  .swiper {
    position: relative;
    display: inline-block;
    width: 100%;
    .wrapper {
      display: inline-flex;
      gap: 24px;
      width: 100%;
      padding-right: 500px;
    }
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
