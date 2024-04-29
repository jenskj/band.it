<script lang="ts" setup>
import type { AlbumInfo } from "~/types";
const { data: value } = await useFetch(
  "https://www.theaudiodb.com/api/v1/json/2/album.php?i=111418"
);
const albumsByYear = computed(() =>
  (value as any)?.value.album?.sort((a: AlbumInfo, b: AlbumInfo) => {
    const yearA = a.intYearReleased;
    const yearB = b.intYearReleased;

    if (yearA && yearB) {
      return yearA < yearB ? yearA : -1;
    }
    return -1;
  })
);
</script>

<template>
  <Page>
    <PageHeader :additional-info="albumsByYear.length" title="Albums" />
    <AlbumList :albums="albumsByYear" />
  </Page>
</template>
