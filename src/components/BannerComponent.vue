<script setup lang="ts">
import { computed, onMounted, onUnmounted, ref } from "vue";
import "vue3-carousel/dist/carousel.css";
import { Carousel, Slide, Navigation } from "vue3-carousel";
import { BannerDTO } from "../types/index";

const props = defineProps<{
  mode: "square" | "rectangle";
  carouselOnMobile: boolean;
  items: Array<BannerDTO>;
}>();

const currentSlide = ref(0);
const isMobile = ref(false);

const galleryImages = computed(() =>
  props.items.filter((items) => items.type == "image")
);
const galleryCTA = computed(() =>
  props.items.find((items) => items.type == "cta")
);

onMounted(() => {
  setScreenType();
  window.addEventListener("resize", setScreenType);
});

onUnmounted(() => {
  window.removeEventListener("resize", setScreenType);
});

function slideTo(val: number) {
  currentSlide.value = val;
}

function openLinkInNewTab(url: string) {
  window.open(url, "_blank");
}

function setScreenType() {
  isMobile.value = window.innerWidth <= 768;
}
</script>

<template>
  <div
    class="banner-component"
    :class="{
      'banner-component_rectangle': mode == 'rectangle',
    }"
  >
    <template v-if="carouselOnMobile && isMobile">
      <div class="banner-component__item">
        <div class="banner-component__item__cta">
          <p class="banner-component__item__cta__title">
            {{ galleryCTA!.title }}
          </p>
          <button
            @click="openLinkInNewTab(galleryCTA!.link)"
            class="banner-component__item__cta__btn"
          >
            {{ galleryCTA!.button }}
          </button>
        </div>
      </div>
      <carousel
        class="banner-component__gallery"
        :items-to-show="1"
        :wrap-around="false"
        v-model="currentSlide"
      >
        <slide
          v-for="(item, index) in galleryImages"
          :key="index"
          class="banner-component__gallery__slide"
        >
          <a
            :href="item.link"
            target="_blank"
            class="banner-component__gallery__slide__link"
          >
            <img
              :src="item.src"
              alt=""
              class="banner-component__gallery__slide__link__img"
            />
          </a>
        </slide>
        <template #addons>
          <Navigation />
        </template>
      </carousel>
      <div class="banner-component__thumbnails">
        <div
          v-for="(image, index) in galleryImages"
          :key="index"
          class="banner-component__thumbnails__item"
          :class="{
            'banner-component__thumbnails__item_selected':
              currentSlide == index,
          }"
          @click="slideTo(index)"
        >
          <img
            :src="image.src"
            alt=""
            class="banner-component__thumbnails__item__img"
          />
        </div>
      </div>
    </template>
    <template v-else>
      <div
        v-for="(item, index) in items"
        :key="index"
        class="banner-component__item"
        :class="{
          'banner-component__item_square':
            mode == 'rectangle' && item.aspectRatio == 'square',
          'banner-component__item_rectangle': item.aspectRatio == 'rectangle',
        }"
      >
        <a
          v-if="item.type == 'image'"
          :href="item.link"
          target="_blank"
          class="banner-component__item__link"
        >
          <img
            :src="item.src"
            alt=""
            class="banner-component__item__link__img"
          />
        </a>
        <div v-else class="banner-component__item__cta">
          <p class="banner-component__item__cta__title">{{ item.title }}</p>
          <button
            @click="openLinkInNewTab(item.link)"
            class="banner-component__item__cta__btn"
          >
            {{ item.button }}
          </button>
        </div>
      </div>
    </template>
  </div>
</template>
