<script lang="ts" setup>
defineProps<{
  title: string;
  additionalInfo?: string;
}>();
</script>

<template>
  <div class="header">
    <div class="header__title-container">
      <h1 class="header__title">{{ title }}</h1>
      <div class="header__additional-info" v-if="additionalInfo">
        ({{ additionalInfo }})
      </div>
    </div>
    <hr class="header__divider" />
  </div>
</template>

<style lang="scss">
.header {
  margin-bottom: 1rem;

  &__divider {
    width: 100%;
    height: 2px;
  }

  &__title {
    margin: 0;
    &-container {
      display: flex;
      align-items: center;
      gap: 1rem;
    }
  }

  &__additional-info {
    font-size: 1.5rem;
    color: lightgray;
  }
}
</style>
