<template>
  <form @submit.prevent="onSubmit">
    <h3>Query options</h3>
    <fieldset role="group">
      <input type="number" id="page-number" v-model="pageNumber" placeholder="Page number" />
      <input type="number" id="per-page" v-model="perPage" placeholder="Per page" />
    </fieldset>
    <details class="dropdown">
      <summary>
        Magnitude types
      </summary>
      <ul>
        <li>
          <label>
            <input type="checkbox" id="md" value="md" v-model="magFilter" />
            MD
          </label>
        </li>
        <li>
          <label>
            <input type="checkbox" id="ml" value="ml" v-model="magFilter" />
            ML
          </label>
        </li>
        <li>
          <label>
            <input type="checkbox" id="ms" value="ms" v-model="magFilter" />
            MS
          </label>
        </li>
        <li>
          <label>
            <input type="checkbox" id="mw" value="mw" v-model="magFilter" />
            MW
          </label>
        </li>
        <li>
          <label>
            <input type="checkbox" id="me" value="me" v-model="magFilter" />
            ME
          </label>
        </li>
        <li>
          <label>
            <input type="checkbox" id="mi" value="mi" v-model="magFilter" />
            MI
          </label>
        </li>
        <li>
          <label>
            <input type="checkbox" id="mb" value="mb" v-model="magFilter" />
            MB
          </label>
        </li>
        <li>
          <label>
            <input type="checkbox" id="mlg" value="mlg" v-model="magFilter" />
            MLG
          </label>
        </li>
      </ul>
    </details>
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
