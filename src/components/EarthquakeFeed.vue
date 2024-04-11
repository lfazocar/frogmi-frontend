<template>
  <div>
    <h1>USGS Earthquake Feed</h1>
    <h2>All Earthquakes from the past 30 days</h2>
    <ul v-if="features">
      <li
        v-for="feature in features"
        :key="feature.id"
      >
        <div>
          <ul>
            <li
              v-for="(attribute, name) in feature.attributes"
              :key="feature.attributes.external_id">
              {{ name }}: {{ attribute }}
            </li>
          </ul>
        </div>
        <div>
          <PostComment @createComment="postNewComment(feature.id, $event)" />
        </div>
      </li>
    </ul>
    <div>
      <p>Current page: {{ pagination.current_page }}</p>
      <p>Features per page: {{ pagination.per_page }}</p>
      <p>Total features in feed: {{ pagination.total }}</p>
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
    const apiUrl = 'http://localhost:3000/api' + fullPath;
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
