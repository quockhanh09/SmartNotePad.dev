<template>
  <div id="wall">
    <h1>Public Wall</h1>
    <h2>You can view the recent posts made by you.</h2>

    <div id="post-list">
      <Post v-for="post in slicedPosts" :key="post.postId" :post-data="post" />
    </div>
  </div>
</template>

<script>
import Post from './Post.vue';
 import './styles/Responsive.css'
export default {
  components: {
    Post
  },
  props: {
    posts: {
      type: Array,
      required: true
    }
  },
  computed: {
    slicedPosts() {
      if (this.posts && Array.isArray(this.posts)) {
        return this.posts.slice(0, 5);
      } else {
        return [];
      }
    }
  }
};
</script>
<style>
/* h1 {
    margin: 0px;
    padding: 0px;
} */
#wall {
    background-color: #161616;
    color: white;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    padding: 50px;
}

#wall h1 {
    margin: 0px;
}

.alert {
    border-left: 5px solid #ea1538 ;
    padding: 10px;
    border-radius: 10px;
    background-color: #1e1e1e;
    display: flex;
    align-items: center;
}

.alert p {
    padding-left: 10px;
}

#post-list {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    width: 100%;
}

#post-author img {
    height: 30px;
    border-radius: 50%;

}
</style>
