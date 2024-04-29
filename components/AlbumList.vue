<script setup lang="ts">
import type { AlbumInfo } from "~/types";
// @ts-ignore
import nuxtStorage from "nuxt-storage";
import CardViewOutline from "../assets/icons/Card view_outline.svg";
import CardViewSolid from "../assets/icons/Card view_solid.svg";
import ListViewOutline from "../assets/icons/List view_outline.svg";
import ListViewSolid from "../assets/icons/List view_solid.svg";

defineProps<{
  albums?: AlbumInfo[];
}>();

const currentView = ref("list");
const toggleView = (newView: string) => {
  currentView.value = newView;
  nuxtStorage.localStorage.setData("view", newView);
};
onMounted(() => {
  const storedView = nuxtStorage.localStorage.getData("view");
  if (storedView) {
    currentView.value = storedView;
  }
});
</script>

<template>
  <div class="album-list">
    <div class="album-list__views">
      <button @click="toggleView('list')">
        <ListViewSolid v-if="currentView === 'list'" />
        <ListViewOutline v-else />
      </button>
      <button @click="toggleView('card')">
        <CardViewSolid v-if="currentView === 'card'" />
        <CardViewOutline v-else />
      </button>
    </div>
    <ul
      v-if="albums"
      class="album-list__container"
      :class="{ 'album-list__container--card': currentView === 'card' }"
    >
      <NuxtLink v-for="album in albums" :to="`/${album.idAlbum || ''}`">
        <AlbumListItem :album-info="album" :view-type="currentView" />
      </NuxtLink>
    </ul>
  </div>
</template>

<style lang="scss">
.album-list {
  display: grid;
  gap: 2rem;

  &__views {
    display: flex;
    justify-content: flex-end;
    align-items: center;
    gap: 1rem;
  }

  &__container {
    display: grid;
    gap: 4rem;
    width: 100%;

    &--card {
      gap: 1rem;
      grid-auto-rows: minmax(232px, 1fr);
      grid-template-columns: repeat(auto-fill, minmax(232px, 1fr));
    }
  }
}
</style>
