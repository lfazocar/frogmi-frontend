<template>
  <form @submit.prevent="onSubmit">
    <h3>Query options</h3>
    <fieldset role="group">
      <input type="number" id="page-number" v-model="pageNumber" placeholder="Page number" />
      <input type="number" id="per-page" v-model="perPage" placeholder="Per page" />
    </fieldset>
    <fieldset>
      <legend>Magnitude types</legend>
      <input type="checkbox" id="md" value="md" v-model="magFilter" />
      <label for="md">MD</label>
      <input type="checkbox" id="ml" value="ml" v-model="magFilter" />
      <label for="ml">ML</label>
      <input type="checkbox" id="ms" value="ms" v-model="magFilter" />
      <label for="ms">MS</label>
      <input type="checkbox" id="mw" value="mw" v-model="magFilter" />
      <label for="mw">MW</label>
      <input type="checkbox" id="me" value="me" v-model="magFilter" />
      <label for="me">ME</label>
      <input type="checkbox" id="mi" value="mi" v-model="magFilter" />
      <label for="mi">MI</label>
      <input type="checkbox" id="mb" value="mb" v-model="magFilter" />
      <label for="mb">MB</label>
      <input type="checkbox" id="mlg" value="mlg" v-model="magFilter" />
      <label for="mlg">MLG</label>
    </fieldset>
    <input type="submit" value="Go" />
  </form>
</template>

<script setup>
import router from '@/router';
import { ref } from 'vue';

const pageNumber = ref('');
const perPage = ref('');
const magFilter = ref([]);

const onSubmit = () => {
  const query = {}
  if(pageNumber.value) { query['page'] = pageNumber.value }
  if(perPage.value) { query['per_page'] = perPage.value }
  if(magFilter.value) { query['mag_type[]'] = magFilter.value }
  router.push({ name: 'features', query: query })
  pageNumber.value = '';
  perPage.value = '';
  magFilter.value = [];
}
</script>
