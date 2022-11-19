<script>
    import Navbar from './components/Navbar.vue';
    import BodyPage from './components/BodyPage.vue';

    export default {
      name: 'App',
      data() {
        return {
          
        }
      },
      components: { Navbar, BodyPage },
      
    }
</script>

<template>
  <Navbar />
  <BodyPage />
</template>

<style scoped>
body {
  background-color: black;
  padding: 0;
  margin: 0;
}

</style>
