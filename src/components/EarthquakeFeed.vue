<template>
  <div>
    <ul class="feature-list" v-if="features">
      <article
        v-for="feature in features"
        :key="feature.id"
      >
        <div>
          <ul>
            <template
              v-for="(value, key) in feature.attributes"
              :key="feature.attributes.external_id"
            >
              <li v-if="(typeof value != 'object')">
                <b>{{ humanizeString(key) }}:</b> {{ value }}
              </li>
              <li v-else>
                <b>{{ humanizeString(key) }}:</b> {{ humanizeString(JSON.stringify(value)) }}
              </li>
            </template>
          </ul>
          <a :href=feature.links.external_url target="_blank">See in the USGS website</a>
        </div>
        <hr />
        <FeatureComments :feature_id="feature.id" />
      </article>
    </ul>
    <div class="grid">
      <p>Current page: <b>{{ pagination.current_page }}</b></p>
      <p>Features per page: <b>{{ pagination.per_page }}</b></p>
      <p>Total features: <b>{{ pagination.total }}</b></p>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { useRoute, onBeforeRouteUpdate } from 'vue-router';
import FeatureComments from './FeatureComments.vue';

const route = useRoute();
const features = ref({});
const pagination = ref({});

const getFeatures = async (fullPath) => {
  try {
    const apiUrl = import.meta.env.VITE_API_URL + fullPath;
    const res = await fetch(apiUrl);
    if(!res.ok) {
      throw new Error('Failed to fetch data');
    }
    const feed = await res.json();
    features.value = feed.data;
    pagination.value = feed.pagination;
  } catch (err) {
    console.error('Error fetching feed data:', err);
  }
}

const humanizeString = function (str){
  return str
    .replace(/[^\w.,:-]/g, '')
    .replace(/[,]/g, ', ')
    .replace(/[:]/g, ': ')
    .replace(/[_]/g, ' ')
    .replace(/\b(?=\w)[a-z]/g, (char) => { return char.toUpperCase(); })
}

getFeatures(route.fullPath);

onBeforeRouteUpdate(async (to, from) => {
  getFeatures(to.fullPath)
});
</script>

<style scoped>
.feature-list {
  padding-left: 0;
}

.grid {
  text-align: center;
}
</style>
