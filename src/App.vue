<template>
  <header-component />
  <main>
    <RouterView />
  </main>
</template>

<script setup>
import { RouterView } from 'vue-router'
import HeaderComponent from './components/HeaderComponent.vue'
</script>

<style>
main {
  padding: 5rem;
}

.test-cont {
  text-align: center;
  border: 1px solid #000;
  border-radius: 0.5rem;
  margin-bottom: 5rem;
  padding: 1%;
}

.list-container,
.pre-container {
  width: max-content;
  margin: 0 auto;
}

@media (max-width: 991px) {
  .list-container,
  .pre-container {
    width: inherit;
  }
}

@media (max-width: 767px) {
  main {
    padding: 2rem;
  }
}
</style>
