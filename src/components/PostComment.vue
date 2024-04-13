<template>
  <details>
    <summary>Leave a comment</summary>
    <form @submit.prevent="onSubmit">
      <input
        type="text"
        id="comment"
        v-model="comment"
        placeholder="Your comment here..."
        required
      />
      <input type="submit" value="Create comment" />
    </form>
  </details>
</template>

<script setup>
import { ref } from 'vue';

const comment = ref('');
const emit = defineEmits(['createComment']);

const onSubmit = () => {
  if(!comment.value) {
    return;
  }
  const newComment = {
    body: comment.value
  }
  comment.value = '';
  emit('createComment', newComment);
}
</script>
