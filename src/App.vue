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

  <hr />
  <footer>
    <p>Made with</p>
    <div>
      <a href="https://rubyonrails.org/" target="_blank">
        <img src="/rails.svg">
      </a>
      <a href="https://vitejs.dev/" target="_blank">
        <img src="/vite.svg">
      </a>
      <a href="https://vuejs.org/" target="_blank">
        <img src="/vue.svg">
      </a>
      <a href="https://picocss.com/" target="_blank">
        <div class="pico-logo"></div>
      </a>
    </div>
  </footer>
</template>

<style scoped>
footer {
  text-align:center;
}

footer > div {
  display: flex;
  align-items: center;
  justify-content: space-evenly;
  margin: 0 20% 1em;
  /* border: 1px solid red; */
}

footer img {
  height: 50px;
}

.pico-logo {
  background-image: url(/pico-logo-dark.svg);
  background-size: contain;
  background-repeat: no-repeat;
  background-position: center;
  width: 100px;
  height: 50px;
}

@media (prefers-color-scheme: light) {
  .pico-logo {
    background-image: url(/pico-logo-light.svg);
  }
}
</style>
