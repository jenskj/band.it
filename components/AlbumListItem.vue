<script setup lang="ts">
import type { AlbumInfo } from "~/types";

defineProps<{
  albumInfo?: AlbumInfo;
  viewType: string;
}>();
</script>

<template>
  <li class="album-list-item" :title="albumInfo?.strAlbum">
    <div v-if="albumInfo" class="album-list-item__content">
      <NuxtLink :to="`/${albumInfo.idAlbum || ''}`">
        <AlbumCover
          :album-info="albumInfo"
          :disable-hover-effect="viewType === 'list'"
        />
      </NuxtLink>

      <div v-if="viewType === 'list'" class="album-list-item__info">
        <h2 class="album-list-item__header">
          {{ `${albumInfo.strAlbum} (${albumInfo.intYearReleased})` }}
        </h2>
        <Rating :album-id="albumInfo.idAlbum" />

        <div
          v-if="albumInfo.strDescriptionEN"
          class="album-list-item__description"
        >
          <p class="album-list-item__description-text">
            {{ albumInfo.strDescriptionEN }}
          </p>
          <NuxtLink :to="`/${albumInfo.idAlbum || ''}`">
            <button
              v-if="albumInfo.strDescriptionEN.length >= 635"
              class="album-list-item__expand-button"
            >
              Read more
            </button>
          </NuxtLink>
        </div>
      </div>
      <div
        v-else-if="viewType === 'list'"
        class="album-list-item__fallback-text"
      >
        No info currently available
      </div>
    </div>
  </li>
</template>

<style lang="scss">
.album-list-item {
  display: grid;
  gap: 1.5rem;

  &__content {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
  }

  &__description {
    display: grid;
    gap: 0.5rem;
    justify-items: flex-start;
  }

  &__description-text {
    max-height: 198px;
    overflow-y: hidden;
    margin: 0;
  }

  &__expand-button {
    margin-top: rem;
    transition: color 100ms ease-in-out;
    text-transform: uppercase;
    &:hover {
      color: rgb(129, 192, 129);
    }
  }

  &__info {
    display: grid;
    gap: 1rem;
  }

  &__header {
    margin: 0;
  }

  &__fallback-text {
    margin-top: 1rem;
    font-size: 1.2rem;
  }
}
</style>
