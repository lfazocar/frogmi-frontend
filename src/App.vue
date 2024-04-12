<script setup>
import { RouterLink, RouterView } from 'vue-router';
import FeedFilter from './components/FeedFilter.vue';
</script>

<template>
  <header>
    <nav>
      <ul>
        <li><strong>Desafío Técnico Frogmi</strong></li>
        <li><RouterLink to="/">Home</RouterLink></li>
      </ul>
    </nav>
    <FeedFilter />
  </header>

  <RouterView />
</template>
