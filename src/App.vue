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

<style scoped>
main {
  margin-top: 5rem;
}
</style>
