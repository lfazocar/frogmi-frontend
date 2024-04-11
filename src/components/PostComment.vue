<template>
  <h3>Comment this feature</h3>
  <form id="form" @submit.prevent="onSubmit">
    <div>
      <label for="text">Comment</label>
      <input type="text" v-model="comment" placeholder="Your comment here...">
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
    console.log('empty form');
    return;
  }
  const newComment = {
    body: comment.value
  }
  comment.value = '';
  emit('createComment', newComment)
}
</script>
