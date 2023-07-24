<template>
  <div class="post" v-if="postData && postData.title && postData.description && postData.author">
    <h1>{{ postData.title }}</h1>
    <p>{{ postData.description }}</p>
    <div id="post-author">
      <img :src="postData.avatarURL" alt="Author Avatar" />
      <p>{{ postData.author }}</p>
    </div>
    <p><em>Posted - {{ formatDate(new Date(postData.timestamp)) }}</em></p>
  </div>
  <div v-else>
    <p>Loading post data...</p>
  </div>
</template>

<script>
import { defineComponent } from 'vue';
import './styles/Responsive.css'

export default defineComponent({
  props: {
    postData: {
      type: Object,
      required: true,
    },
  },
  methods: {
    formatDate(date) {
      const options = { year: 'numeric', month: 'long', day: 'numeric' };
      return new Date(date).toLocaleDateString(undefined, options);
    },
  },
});
</script>






<style>

.post {
    background-color: #1e1e1e;
    padding: 30px;
    padding-bottom: 10px;
    border-radius: 15px;
    margin-top: 20px;
    width: 60%
}

#post-author {
    display: flex;
    align-items: center;
}

#post-author img {
    margin-right: 10px;
}
  
</style>
