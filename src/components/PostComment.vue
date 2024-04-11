<template>
  <h3>Comment this feature</h3>
  <form id="form" @submit.prevent="onSubmit">
    <div>
      <label for="comment">Comment</label>
      <input type="text" id="comment" v-model="comment" placeholder="Your comment here...">
    </div>
    <button>Create comment</button>
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
