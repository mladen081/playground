<template>
  <button class="fancy-btn">
    <slot>Button</slot>
  </button>
</template>

<style scoped>
.fancy-btn {
  color: #000;
  font-size: 1.8rem;
  background-color: transparent;
  border: 1px solid #000;
  padding: 1rem 2rem;
  margin: 2rem;
  border-radius: 0.5rem;
  cursor: pointer;
}

.fancy-btn:hover,
.fancy-btn:focus {
  background-color: #c21010;
  border: 1px solid #c21010;
  color: #fff;
}
</style>
