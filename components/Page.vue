<template>
  <div class="page">
    <slot />
  </div>
</template>

<style lang="scss">
.page {
  display: grid;
  gap: 1rem;
  max-width: 768px;
  height: 100%;
  margin: auto;
  padding: 1rem;
}
</style>
