<script setup>
import Navbar from './components/Navbar.vue';
import BodyPage from './components/BodyPage.vue'
</script>

<template>
  <Navbar />
  <div class="test">
    <BodyPage />
  </div>
</template>

<style scoped>
body {
  background-color: black;
  padding: 0;
  margin: 0;
}
.test {
  background-color: rgb(240, 238, 238);
  height: 100vh;
  margin: 0;
}
</style>
