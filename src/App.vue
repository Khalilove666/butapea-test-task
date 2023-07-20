<script setup lang="ts">
import BannerComponent from "./components/BannerComponent.vue";
import { BannerDTO } from "./types";

const items: Array<BannerDTO> = [
  {
    type: "image",
    aspectRatio: "square",
    src: "https://picsum.photos/400",
    link: "https://example.com/link1",
  },
  {
    type: "cta",
    title: "CTA Title",
    button: "CTA Button",
    link: "https://example.com/link2",
  },
  {
    type: "image",
    aspectRatio: "square",
    src: "https://picsum.photos/400",
    link: "https://example.com/link3",
  },
];
const items2: Array<BannerDTO> = [
  {
    type: "cta",
    title: "CTA Title",
    button: "CTA Button",
    link: "https://example.com/link1",
  },
  {
    type: "image",
    aspectRatio: "square",
    src: "https://picsum.photos/400",
    link: "https://example.com/link2",
  },
  {
    type: "image",
    aspectRatio: "square",
    src: "https://picsum.photos/400",
    link: "https://example.com/link3",
  },
  {
    type: "image",
    aspectRatio: "square",
    src: "https://picsum.photos/400",
    link: "https://example.com/link3",
  },
  {
    type: "image",
    aspectRatio: "square",
    src: "https://picsum.photos/400",
    link: "https://example.com/link3",
  },
  {
    type: "image",
    aspectRatio: "square",
    src: "https://picsum.photos/400",
    link: "https://example.com/link3",
  },
];
const items3: Array<BannerDTO> = [
  {
    type: "image",
    aspectRatio: "rectangle",
    src: "https://picsum.photos/1200/400",
    link: "https://example.com/link1",
  },
  {
    type: "image",
    aspectRatio: "square",
    src: "https://picsum.photos/400",
    link: "https://example.com/link1",
  },
  {
    type: "cta",
    title: "CTA Title",
    button: "CTA Button",
    link: "https://example.com/link1",
  },
];
</script>

<template>
  <div class="container">
    <h1 class="mt-4 mb-4">Banner 1</h1>
    <banner-component
      mode="square"
      :carousel-on-mobile="false"
      :items="items"
    />
    <h1 class="mt-4 mb-4">Banner 2</h1>
    <banner-component
      mode="square"
      :carousel-on-mobile="true"
      :items="items2"
    />
    <h1 class="mt-4 mb-4">Banner 3</h1>
    <banner-component
      mode="rectangle"
      :carousel-on-mobile="false"
      :items="items3"
    />
  </div>
</template>
