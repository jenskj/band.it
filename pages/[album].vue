<script setup lang="ts">
import type { AlbumInfo } from "~/types";
import ArrowBack from "../assets/icons/arrow-back.svg";
const { params } = useRoute();

const {
  data: { value },
} = await useFetch(
  `https://www.theaudiodb.com/api/v1/json/2/album.php?m=${params.album}`
);
const albumData: AlbumInfo = (value as any).album[0];
</script>

<template>
  <Page>
    <PageHeader
      :additional-info="albumData.intYearReleased"
      :title="albumData.strAlbum || 'Unknown'"
    />
    <div class="album-details__options">
      <NuxtLink to="/"><ArrowBack /> Go back</NuxtLink>
    </div>
    <AlbumCover
      :cover-url="albumData.strAlbumThumb"
      :album-name="albumData.strAlbum"
      :disable-hover-effect="true"
    />

    <div class="album-details__info">
      <div
        v-if="albumData.strDescriptionEN"
        class="album-details__info-section"
      >
        <h2>Description</h2>
        <p>
          {{ albumData.strDescriptionEN }}
        </p>
      </div>
      <div
        v-if="
          albumData.strReview &&
          albumData.strReview !== albumData.strDescriptionEN
        "
        class="album-details__info-section"
      >
        <h2>Review</h2>
        <p>
          {{ albumData.strReview }}
        </p>
      </div>
    </div>
  </Page>
</template>

<style lang="scss">
.album-details {
  &__options {
    a {
      display: flex;
      align-items: center;
      gap: 0.5rem;
    }
  }

  &__info {
    display: grid;
    gap: 0.5rem;
    &-section {
    }
  }
}
</style>
