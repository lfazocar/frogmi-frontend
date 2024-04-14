<template>
  <details>
    <summary>Leave a comment</summary>
    <form @submit.prevent="postComment">
      <input
        type="text"
        id="comment"
        v-model="newComment"
        placeholder="Your comment here..."
        required
      />
      <input type="submit" value="Create comment" />
    </form>
  </details>
  <details @click.once="getComments">
    <summary>Show comments</summary>
      <p v-if="!featureComments.length">No comments found</p>
        <ul v-if="featureComments.length">
          <li
            v-for="comment in featureComments"
            :key="comment.id"
          >
            {{ comment.body }}
          </li>
        </ul>
  </details>
</template>

<script setup>
import { ref } from 'vue';
import { useToast } from 'vue-toastification';
import { useRoute } from 'vue-router';
const route = useRoute();
const toast = useToast();

const props = defineProps({
  feature_id: String
})
const featureComments = ref([]);
const newComment = ref('');

const postComment = async () => {
  try {
    if(!newComment.value) {
      toast.error("Can't submit empty comment!");
      return;
    }
    const requestBody = {
      body: newComment.value
    }
    const apiUrl = import.meta.env.VITE_API_URL + route.path + `/${props.feature_id}/comments`;
    const res = await fetch(apiUrl, {
      method: 'POST',
      headers: {
        'content-type': 'application/json'
      },
      body: JSON.stringify(requestBody)
    });
    newComment.value = '';
    toast.success("Comment created!");
    getComments(props.feature_id)
    if(!res.ok) {
      throw new Error('Failed to post comment');
    }
  } catch (err) {
    console.error('Error creating comment:', err);
  }
};

const getComments = async () => {
  try {
    const apiUrl = import.meta.env.VITE_API_URL + route.path + `/${props.feature_id}/comments`;
    const res = await fetch(apiUrl);
    if(!res.ok) {
      throw new Error('Failed to fetch comments');
    }
    featureComments.value = await res.json();
  } catch (err) {
    console.error('Error fetching comments:', err);
  }
}
</script>
