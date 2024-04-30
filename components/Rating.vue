<script setup lang="ts">
/**
 * This is merely a demonstration of what a rating system might look like in the frontend, using localStorage as a dummy backend. It is apparently possible to add user ratings on AudioDB, but their user signup is currently disabled. Had this not been the case, I would naturally have built the rating system around that API.
 */

// @ts-ignore
import nuxtStorage from "nuxt-storage";
import Star from "../assets/icons/star.svg";
import StarOutline from "../assets/icons/star-outline.svg";

const props = defineProps<{
  albumId?: string;
  fixedRating?: number;
}>();

onMounted(() => {
  if (!props.fixedRating) {
    updateCurrentRating();
  } else {
    currentRating.value = props.fixedRating;
  }
});

const currentRating = ref(0);

const updateCurrentRating = () => {
  const storedRatings = nuxtStorage.localStorage.getData("ratings");
  const ratings = JSON.parse(storedRatings) || {};
  if (ratings && props.albumId) {
    const albumRating = ratings[props.albumId];
    if (albumRating) {
      currentRating.value = albumRating;
    }
  }
};

const submitRating = (newRating: number) => {
  if (props.fixedRating) {
    return;
  }
  const storedRatings = nuxtStorage.localStorage.getData("ratings");
  const ratings = JSON.parse(storedRatings) || {};
  const newRatingIsValid = newRating && newRating > 0 && newRating < 6;
  if (newRatingIsValid && props.albumId) {
    if (ratings) {
      // If the ratings object already exists in storage, we update it
      const newRatings = {
        ...ratings,
        [props.albumId]: newRating,
      };
      nuxtStorage.localStorage.setData("ratings", JSON.stringify(newRatings));
    } else {
      // If not, we create it
      const newRatings = { [props.albumId]: newRating };
      nuxtStorage.localStorage.setData("ratings", JSON.stringify(newRatings));
    }
    updateCurrentRating();
  }
};
</script>

<template>
  <div class="rating">
    <h3 v-if="fixedRating" class="rating__title">
      {{ currentRating ? "Official rating" : "No official rating" }}
    </h3>
    <h3 v-else class="rating__title">
      {{ currentRating ? "My current rating" : "Rate this album!" }}
    </h3>
    <div class="rating__stars">
      <Star
        v-for="(star, index) in currentRating"
        @click="submitRating(index + 1)"
      />
      <StarOutline
        v-for="(star, index) in 5 - currentRating"
        @click="submitRating(currentRating + index + 1)"
      />
    </div>
  </div>
</template>

<style lang="scss">
.rating {
  display: grid;
  gap: 0.5rem;
  &__title {
    margin: 0;
  }
}
</style>
