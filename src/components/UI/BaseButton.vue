<template>
  <button :type="type" :class="mode">
      <slot></slot>
  </button>
</template>

<script>
export default {
    props: ['type', 'mode']
}
</script>

<style scoped>
button {
  padding: 0.75rem 1.5rem;
  font-family: inherit;
  font-weight: bold;
  background-color: #3700B3;
  border: 1px solid #3700B3;
  border-radius: 5px;
  color: white;
  cursor: pointer;
}

button:hover,
button:active {
  background-color: #6200EE;
  border-color: #6200EE;
}

.flat {
  background-color: transparent;
  color: #3700B3;
  border: none;
}

.flat:hover,
.flat:active {
  background-color: #edd2ff;
}
</style>