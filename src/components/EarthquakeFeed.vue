<template>
  <div>
    <ul v-if="features">
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
        <PostComment @createComment="postNewComment(feature.id, $event)" />
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
import PostComment from './PostComment.vue';

const route = useRoute();
const features = ref({});
const pagination = ref({});

const refreshFeed = async (fullPath) => {
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

refreshFeed(route.fullPath);

onBeforeRouteUpdate(async (to, from) => {
  refreshFeed(to.fullPath)
});

const postNewComment = async (feature_id, comment) => {
  try {
    const res = await fetch(`http://localhost:3000/api/features/${feature_id}/comments`, {
      method: 'POST',
      headers: {
        'content-type': 'application/json'
      },
      body: JSON.stringify(comment)
    });
    if(!res.ok) {
      throw new Error('Failed to post comment');
    }
  } catch (err) {
    console.error('Error creating comment:', err);
  }
};
</script>

<style scoped>
.grid {
  text-align: center;
}
</style>
