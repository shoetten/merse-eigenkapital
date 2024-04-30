<script setup lang="ts">
import DonationBar from './components/DonationBar.vue'
import Badge from './components/Badge.vue'
</script>

<template>
  <main>
    <Badge>Gekauft</Badge>
    <DonationBar class="bar" />
    <a class="btn" href="https://merse88b.de/unterstuetzen/">
      Jetzt unterstützen!
    </a>
  </main>
</template>

<style scoped>
main {
  display: flex;
  flex-direction: column;
  place-items: center;
  justify-content: center;
  gap: 2rem;
  position: relative;
  width: 100%;
  max-width: 800px;
  min-height: 100vh;
  overflow: hidden;
  padding: 2rem;

  &::before {
    content: '';
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    z-index: -1;
    background-image: url('/hausfoto_web_large.jpg');
    background-size: cover;
    background-position: center 25%;
  }

  background-color: rgba(0, 0, 0, 0.3);

  @media screen and (min-width: 800px) {
    min-height: 90vh;
    border-radius: 1rem;
  }
}

.bar {
  min-height: max(550px, 60vh);
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
