<script setup lang="ts">
import type { AlbumInfo } from "~/types";
import CardViewOutline from "../assets/icons/Card view_outline.svg";
import CardViewSolid from "../assets/icons/Card view_solid.svg";
import ListViewOutline from "../assets/icons/List view_outline.svg";
import ListViewSolid from "../assets/icons/List view_solid.svg";

defineProps<{
  albums?: AlbumInfo[];
}>();
</script>

<template>
  <div class="album-list">
    <div class="album-list__views">
      <button class="album-list__views-button"><CardViewOutline /></button>
      <button class="album-list__views-button"><ListViewOutline /></button>
    </div>
    <div v-if="albums" class="album-list__container">
      <AlbumListItem v-for="album in albums" :album-info="album" />
    </div>
  </div>
</template>

<style lang="scss">
.album-list {
  display: grid;
  gap: 1rem;

  &__views {
    display: flex;
    justify-content: flex-end;
    align-items: center;
    gap: 0.5rem;

    &-button {
    }
  }

  &__container {
    display: grid;
    gap: 1rem;
    grid-template-columns: repeat(auto-fill, minmax(240px, 1fr));
    grid-auto-rows: minmax(240px, 1fr);
    width: 100%;
  }
}
</style>
