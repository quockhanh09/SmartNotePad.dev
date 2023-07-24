<template>
  <div class="app">
    <SignInModal :display="displayModal" @toggle="toggleModal" />
    <NavBar :toggle="toggleModal" :logged_in="user ? true : false" />
    <template v-if="user">
      <NewPost :onUpdate="handleUpdate" :toggle="toggleModal" />
    </template>
    <template v-else>
      <SignIn />
    </template>
    <Wall :posts="posts" />
    <Footer />
  </div>
</template>

<script>
import { ref, reactive, computed, onMounted } from 'vue';

import NavBar from './components/NavBar.vue';
import NewPost from './components/NewPost.vue';
import Wall from './components/Wall.vue';
import Footer from './components/Footer.vue';
import SignIn from './components/SignIn.vue';
import SignInModal from './components/SignInModal.vue';
import { authentication } from './services/firebase-config';
import logo from './images/logo.png';

let posts = [
  {
    id: '1',
    title: 'Demo Post!',
    description: 'This is a post to demonstrate where your posts will show up!',
    timestamp: new Date().toISOString(),
    author: 'SmartNotePad- System',
    postId: 'DEFAULT_POST',
    avatarURL: logo,
  },
];

export default {
  components: {
    NavBar,
    NewPost,
    Wall,
    Footer,
    SignIn,
    SignInModal,
  },
  setup() {
    const displayModal = ref(false);
    const user = ref(null);
    const post = reactive(posts);

    authentication.onAuthStateChanged((authUser) => {
      user.value = authUser;
    });

    const handleUpdate  = (newPosts) => {
      if (newPosts?.length > 1) {
        post.push(...newPosts);
      } else {
        post.unshift(newPosts);
      }
    };

    const toggleModal = () => {
      displayModal.value = !displayModal.value;
    };

    return {
      displayModal,
      user,
      posts,
      handleUpdate ,
      toggleModal,
    };
  },
};
</script>

<style>


.app{
  background-color: #282c34;
  display: flex;
  flex-direction: column;
  justify-content: center;
  text-align: center;
  color: white;
}

</style>
