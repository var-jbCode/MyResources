<template>
  <button :type="type" :class="mode">
    <slot />
  </button>
</template>

<script>
export default {
  props: ['type', 'mode'],
};
</script>

<style scoped>
button {
  padding: 0.75rem 1.5rem;
  font-family: inherit;
  background-color: #41b883;
  border: 1px solid #41b883;
  color: white;
  cursor: pointer;
}
button:hover,
button:active {
  background-color: #34495e;
  border-color: #34495e;
}
.flat {
  background-color: transparent;
  color: #41b883;
  border: none;
}
.flat:hover,
.flat:active {
  background-color: #34495e;
}
</style>
