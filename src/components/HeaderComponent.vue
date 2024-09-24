<template>
  <header>
    <nav class="tabs">
      <ul>
        <li>
          <router-link to="/">Home</router-link>
        </li>

        <li>
          <router-link to="/about">About</router-link>
        </li>
      </ul>
    </nav>
  </header>
</template>

<script setup></script>

<style scoped>
header {
  width: 100%;
  position: fixed;
  top: 0;
  z-index: 1000;
  background-color: #fff;
  border-bottom: 1px solid #000;
}

.tabs ul {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 1rem;
  list-style-type: none;
}

.tabs ul li {
  padding: 1rem 0;
}
.tabs ul li a {
  font-size: 3rem;
  font-weight: 300;
}

@media (max-width: 1400px) {
  .tabs ul li a {
    font-size: 2rem;
  }
}

@media (max-width: 1200px) {
}

@media (max-width: 1024px) {
}

@media (max-width: 991px) {
}

@media (max-width: 767px) {
}
</style>
