<template>
  <div class="SocialPostComments">
    <template v-if="comments.length === 0">
      <p>There are no comments for this post!</p>
    </template>
    <template v-else>
      <p>Comments:</p>
      <div v-for="{owner, message} in comments" class="comment" :key="owner">
        <p>{{ owner.firstName }}: <strong>{{ message }}</strong></p>
      </div>
    </template>
  </div>
</template>

<script setup >
import { reactive } from 'vue';
const props = defineProps({
  postId: String
});

const comments = reactive([]);
const fetchComments = async (postId) => {
  const baseUrl = "https://dummyapi.io/data/v1";
  const response = await fetch(`${baseUrl}/post/${postId}/comment?limit=5`,
    {
      "headers": {
        "app-id": "657a3106698992f50c0a5885"
      }
    });
  const result_1 = await response.json();
  Object.assign(comments, result_1.data);
};
await fetchComments(props.postId);
</script>

<style lang="scss">
.SocialPostComments{
  padding-left:24px;
  p {
    font-weight: bold;
  }
  .comment {
    display:flex;
    justify-content: space-between;
    background-color: var(--color-input-mute);
    border-radius: 10px;
    margin-bottom: 8px;
    padding:8px 16px;
    color:var(--color-background-soft);
    width: 75%;
  }
  svg {
    fill:var(--color-background-mute);
  }
}
</style>
