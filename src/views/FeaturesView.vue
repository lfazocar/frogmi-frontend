<template>
  <main>
    <hgroup>
      <h1>USGS Earthquake Feed</h1>
      <p>All Earthquakes from the past 30 days</p>
    </hgroup>
    <EarthquakeFeed />
  </main>
</template>

<script setup>
import EarthquakeFeed from '@/components/EarthquakeFeed.vue';
</script>
