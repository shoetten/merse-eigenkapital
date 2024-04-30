<script setup lang="ts">

</script>

<template>
  <div class="badge">
    <slot />
  </div>
</template>

<style scoped>
.badge {
  background-color: var(--color-secondary);
  text-transform: uppercase;
  padding: 0.5rem 4rem;
  font-weight: bold;
  font-size: 1.6rem;

  position: absolute;
  z-index: 99;
  top: 0;
  left: 0;
  transform: rotate(-40deg) translate(-25%);

  &::before,
  &::after {
    content: '';
    display: block;
    position: absolute;
    z-index: -1;
    top: 0;
    width: 100%;
    height: 100%;
    background-color: var(--color-secondary);
  }
  &::before {
    left: -100%;
  }
  &::after {
    left: 100%;
  }
}
</style>
