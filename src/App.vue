<template>
  <the-header title="Resource Me"></the-header>
  <the-resource></the-resource>
</template>

<script>
import TheHeader from './components/layout/TheHeader.vue';
import TheResource from './components/learning-resource/TheResource.vue';

export default {
  components: {
    TheHeader,
    TheResource
  },
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Archivo:wght@100&display=swap');
* {
  box-sizing: border-box;
}

html {
  font-family: 'Archivo', sans-serif;
}

body {
  margin: 0;
  background-color: #6200EE;
}
</style>