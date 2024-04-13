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
import { useToast } from 'vue-toastification';

const comment = ref('');
const toast = useToast();
const emit = defineEmits(['createComment']);

const onSubmit = () => {
  if(!comment.value) {
    toast.error("Can't submit empty comment!");
    return;
  }
  const newComment = {
    body: comment.value
  }
  comment.value = '';
  toast.success("Comment created!");
  emit('createComment', newComment);
}
</script>
