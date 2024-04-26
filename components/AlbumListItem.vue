<script setup lang="ts">
import type { AlbumInfo } from "~/types";

defineProps<{
  albumInfo?: AlbumInfo;
}>();
</script>

<template>
  <div v-if="albumInfo" class="album-list-item">
    <div>{{ albumInfo?.strAlbum }}</div>
  </div>
</template>

<style lang="scss">
.album-list-item {
  background-color: orange;
}
</style>
