<template>
  <main>
    <CardSearch />
  </main>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import CardSearch from './components/CardSearch.vue';

export default defineComponent({
  name: 'App',
  components: {
    CardSearch
  }
});
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap');

main {
  background: linear-gradient(179.16deg, #000227 16.6%, #0B13A9 99.32%);
  height: 100vh;
  width: 100vw;
  display: flex !important;
  justify-content: center;
  align-items: center;
  font-family: 'Inter', sans-serif;
}
</style>
