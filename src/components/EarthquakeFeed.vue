<template>
  <div>
    <h1>USGS Earthquake Feed</h1>
    <h2>All Earthquakes from the past 30 days</h2>
    <ul v-if="feed">
      <li
        v-for="earthquake in feed.data"
        :key="earthquake.id"
      >
        {{ earthquake }}
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const feed = ref({});

onMounted(async () => {
  try {
    const res = await fetch('http://localhost:3000/api/features?page=1&per_page=2%27');
    if(!res.ok) {
      throw new Error('Failed to fetch data');
    }
    feed.value = await res.json();
  } catch (err) {
    console.error('Error fetching feed data:', err);
  }
});
</script>
