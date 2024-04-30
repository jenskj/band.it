<script setup lang="ts">
import type { AlbumInfo } from "~/types";

defineProps<{
  albumInfo?: AlbumInfo;
  disableHoverEffect?: boolean;
}>();
</script>

<template>
  <div
    v-if="albumInfo"
    class="album-cover__container"
    :class="{
      'album-cover__container--hover-effect': !Boolean(disableHoverEffect),
    }"
  >
    <img
      :src="
        albumInfo.strAlbumThumb
          ? albumInfo.strAlbumThumb
          : 'https://mtclinic.org/wp-content/uploads/2021/09/Photo-Unavailable.jpg'
      "
      :alt="albumInfo.strAlbum || ''"
      class="album-cover"
    />
  </div>
</template>

<style lang="scss">
.album-cover {
  height: 100%;
  width: 100%;
  object-fit: cover;
  position: relative;
  box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;

  &__container {
    aspect-ratio: 1/1;

    &--hover-effect {
      transition-property: transform, opacity;
      transition-duration: 100ms;
      transition-timing-function: cubic-bezier(0.34, 0.5, 0.99, 0.74);
      &:hover {
        transform: scale(1.05);
      }
    }
  }
}
</style>
