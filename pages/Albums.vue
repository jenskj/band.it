<script lang="ts" setup>
import type { AlbumInfo } from "~/types";
const nick = "112452";
const { data: value } = (await useFetch(
  "https://www.theaudiodb.com/api/v1/json/2/searchalbum.php?s=radiohead"
)) as any;
console.log(value.value.album);
const albumsByYear = computed(() =>
  (value as any)?.value.album?.sort((a: AlbumInfo, b: AlbumInfo) => {
    const yearA = a.intYearReleased;
    const yearB = b.intYearReleased;

    if (yearA && yearB) {
      return yearA > yearB ? yearA : -1;
    }
    return -1;
  })
);
</script>

<template>
  <Page>
    <PageHeader :count="albumsByYear.length" title="Albums" />
    <AlbumList :albums="albumsByYear" />
  </Page>
</template>
