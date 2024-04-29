<script setup lang="ts">
defineProps<{
  coverUrl?: string;
  albumName?: string;
  disableHoverEffect?: boolean;
}>();
</script>

<template>
  <div
    class="album-cover__container"
    :class="{
      'album-cover__container--hover-effect': !Boolean(disableHoverEffect),
    }"
  >
    <img
      :src="coverUrl ? coverUrl : 'https://mtclinic.org/wp-content/uploads/2021/09/Photo-Unavailable.jpg'"
      :alt="albumName || ''"
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
