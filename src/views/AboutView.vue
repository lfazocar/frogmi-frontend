<template>
  <div class="about">
    <h1>This is an about page</h1>
    <EarthquakeFeed />
  </div>
</template>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>

<script setup>
import EarthquakeFeed from '@/components/EarthquakeFeed.vue';
</script>
