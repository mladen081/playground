<template>
  <button class="fancy-btn-x">
    <slot>ButtonX</slot>
  </button>
</template>

<style scoped>
.fancy-btn-x {
  color: #000;
  font-size: 1.8rem;
  background-color: transparent;
  border: 1px solid #000;
  padding: 0.5rem;
  margin: 1rem;
  border-radius: 0.5rem;
  cursor: pointer;
}

.fancy-btn-x:hover,
.fancy-btn-xfocus {
  background-color: #c21010;
  border: 1px solid #c21010;
  color: #fff;
}
</style>
