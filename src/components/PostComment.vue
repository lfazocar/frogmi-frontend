<template>
  <form @submit.prevent="onSubmit">
    <label for="comment">Comment this feature</label>
    <input
      type="text"
      id="comment"
      v-model="comment"
      placeholder="Your comment here..."
      required
    />
    <input type="submit" value="Create comment" />
  </form>
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
