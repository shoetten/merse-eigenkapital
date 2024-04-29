<script setup lang="ts">
import DonationBar from './components/DonationBar.vue'
</script>

<template>
  <main>
    <DonationBar />
    <a class="btn" href="https://merse88b.de/unterstuetzen/">
      Jetzt unterstützten!
    </a>
  </main>
</template>

<style scoped>
main {
  display: flex;
  flex-direction: column;
  place-items: center;
  gap: 2rem;
}

button, .btn {
  border-radius: 8px;
  border: 2px solid transparent;
  padding: 0.8em 1.6em;
  font-size: 1.2em;
  font-weight: bold;
  font-family: inherit;
  background-color: #1a1a1a;
  cursor: pointer;
  transition: border-color 0.25s;
  text-decoration: none;

  &:hover {
    border-color: var(--color-secondary);
  }
  &:focus,
  &:focus-visible {
    outline: 4px auto -webkit-focus-ring-color;
  }
}
</style>
