<script setup lang="ts">
import type { AlbumInfo } from "~/types";
import ArrowBack from "../assets/icons/arrow-back.svg";
const { params } = useRoute();

const {
  data: { value },
} = await useFetch(
  `https://www.theaudiodb.com/api/v1/json/2/album.php?m=${params.album}`
);
const albumInfo: AlbumInfo = (value as any).album[0];
</script>

<template>
  <Page>
    <PageHeader
      :additional-info="albumInfo.intYearReleased?.toString()"
      :title="albumInfo.strAlbum || 'Unknown'"
    />
    <div class="album-details__options">
      <NuxtLink to="/"><ArrowBack /> Go back</NuxtLink>
    </div>
    <AlbumCover :album-info="albumInfo" :disable-hover-effect="true" />

    <div class="album-details__info">
      <Rating
        v-if="albumInfo.intScoreVotes"
        :fixed-rating="parseInt(albumInfo.intScoreVotes)"
      />
      <Rating :album-id="albumInfo.idAlbum" />
      <div
        v-if="albumInfo.strDescriptionEN"
        class="album-details__info-section"
      >
        <h3>Description</h3>
        <p>
          {{ albumInfo.strDescriptionEN }}
        </p>
      </div>
      <div
        v-if="
          albumInfo.strReview &&
          albumInfo.strReview !== albumInfo.strDescriptionEN
        "
        class="album-details__info-section"
      >
        <h3>Review</h3>
        <p>
          {{ albumInfo.strReview }}
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
  }
}
</style>
