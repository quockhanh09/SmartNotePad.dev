<template>
  <div id="newpost">
    <h1>What is on your <span>mind</span>?</h1>
    <form @submit.prevent="handleUpdate">
      <textarea class="form-primary" placeholder="Title your post!" v-model="title"></textarea>
<textarea class="form-secondary" placeholder="Content..." v-model="description"></textarea>

      <button type="submit">Post to your Wall!</button>
    </form>
  </div>
</template>

<script>
import { authentication } from "../services/firebase-config";
import anonymous from '../images/default.png';
import { addPost } from "../services/firebase";
import './styles/Responsive.css';

export default {
  data() {
    return {
      title: '',
      description: '',
    };
  },
  methods: {
    magic(input) {
      input = input.replace(/&/g, '&amp;');
      input = input.replace(/</g, '&lt;');
      input = input.replace(/>/g, '&gt;');
      return input;
    },
    async handleUpdate() {
      const post = {
        id: `${authentication.currentUser.uid}-${Math.floor(100000 + Math.random() * 900000)}`,
        title: this.magic(this.title),
        description: this.magic(this.description),
        avatarURL: authentication.currentUser.photoURL ? authentication.currentUser.photoURL : anonymous,
        timestamp: new Date().toISOString(),
        author: authentication.currentUser.displayName ? authentication.currentUser.displayName : 'Demo User',
      };

      console.log("Post data:", post); // Debugging line

      // Call the parent component's onUpdate method
      this.onUpdate(post);

      // Call the addPost function to store the post in Firebase
      addPost(post).then(() => {
        console.log("Post added successfully!"); // Debugging line
      }).catch((error) => {
        console.error("Error adding post:", error); // Debugging line
      });

      // Clear the form after submitting
      this.title = '';
      this.description = '';
    },
  },
  props: {
    onUpdate: {
      type: Function,
      required: true,
    },
  },
};
</script>


<style scoped>

#newpost {
    background-color: #393939;
    color: white;
    text-align: center;
    padding: 10px;
}

#newpost h1 span {
    color: #ea1538;
}

form {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
}

button[type="submit"] {
    padding: 20px 40px;
    font-size: 20px;
    width: 40%;
    margin-bottom: 15px;
} 

textarea {
    border: none;
    color: white;
    width: 40%;
    padding: 10px;
    resize: none;
    font-size: 18px;
}

.form-primary {
    border-radius: 10px 10px 0px 0px;
    border-right: 4px solid #ea1538;
    height: 45px;
    background-color: rgba(0,0,0,0.6);
    padding: 13px 0;
    padding-left: 10px;
    overflow: hidden;
}

.form-secondary {
    border-radius: 0px 0px 10px 10px;
    margin-bottom: 25px;
    height: 175px;
    border-right: 4px solid #ea1538;
    border-bottom: 4px solid #ea1538;
    background-color: rgba(0,0,0,0.4);
}

textarea:focus {
    outline: none;
    border-bottom: 4px solid #ea1538;
    border-right: 4px solid #ea1538;
}

textarea::-webkit-scrollbar {
    width: 1em;
}

textarea::-webkit-scrollbar-track {
    -webkit-box-shadow: inset 0 0 6px rgba(0,0,0,0.3);
            box-shadow: inset 0 0 6px rgba(0,0,0,0.3);
}

textarea::-webkit-scrollbar-thumb {
  background-color: #800015;
}
.image-upload {
    color: white;
    border-right: 4px solid #ea1538;
    width: 579px;
    height: 45px;
    background-color: rgba(0,0,0,0.6);
    padding: 13px 0;
    padding-left: 10px;
    overflow: hidden;
  }
  /* magic(input) {
      input = input.replace(/&/g, '&amp;');
      input = input.replace(/</g, '&lt;');
      input = input.replace(/>/g, '&gt;');
      return input;
    }, */
</style>
