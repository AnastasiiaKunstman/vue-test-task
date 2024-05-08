<template>
  <Header />
  <Widget />
  <Footer />
</template>

<script setup lang="ts">
import { useStore } from './stores/stores';
import Header from './components/ui/Header.vue';
import Footer from './components/ui/Footer.vue';
import Widget from './components/Widget.vue';

const store = useStore();

store.loadItemsFromLocalStorage();
</script>

<style src="./css/index.css"></style>