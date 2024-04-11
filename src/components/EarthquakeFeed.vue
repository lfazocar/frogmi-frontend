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
      <p>Page: {{ pagination.current_page }}</p>
      <p>Features per page: {{ pagination.per_page }}</p>
      <p>Total features: {{ pagination.total }}</p>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import PostComment from './PostComment.vue';

const features = ref({});
const pagination = ref({})
onMounted(async () => {
  try {
    const res = await fetch('http://localhost:3000/api/features?page=1&per_page=2%27');
    if(!res.ok) {
      throw new Error('Failed to fetch data');
    }
    const feed = await res.json();
    features.value = feed.data;
    pagination.value = feed.pagination;
  } catch (err) {
    console.error('Error fetching feed data:', err);
  }
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
