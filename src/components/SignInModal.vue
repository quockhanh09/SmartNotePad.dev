<template>
  <div v-if="display && !isLoggedIn" id="signinmodal">
    <div id="signinmodal-child">
      <h1>Sign In!</h1>
      <p>You can sign in using your Google Account! We also provide a Demo Account for ease-of-access while testing out the site.</p>
      <div id="signin-buttons">
        <div id="google" @click="signInWithGoogle">
          <div id="google-child">
            <img src="../images/google.svg" alt="Google Logo" />
          </div>
          <span>Sign in with Google</span>
        </div>

        <div id="github" @click="signInWithGithub">
          <div id="github-child">
            <img src="../images/github.svg" alt="GitHub Logo" />
          </div>
          <span>Sign in with GitHub</span>
        </div>
        <div id="demo" @click="signInDemo">User</div>
      </div>
      <p @click="toggle" id="nevermind-link">Never mind, I don't want to sign in.</p>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';
import { signInWithPopup, GoogleAuthProvider, GithubAuthProvider, signInAnonymously } from 'firebase/auth';
import { authentication } from '../services/firebase-config';
import './styles/Responsive.css'
export default {
  props: {
    display: Boolean,
    toggle: Function,
  },
  setup(props) {
    const isLoggedIn = ref(false); 
    const signInWithGoogle = () => {
      const provider = new GoogleAuthProvider();
      signInWithPopup(authentication, provider)
        .then((result) => {
          console.log('Google sign-in success', result);
          isLoggedIn.value = true; 
          props.toggle();
        })
        .catch((error) => {
          console.error('Google sign-in error', error);
        });
    };

    const signInWithGithub = () => {
      const provider = new GithubAuthProvider();
      signInWithPopup(authentication, provider)
        .then((result) => {
          console.log('GitHub sign-in success', result);
          isLoggedIn.value = true;
          props.toggle();
        })
        .catch((error) => {
          console.error('GitHub sign-in error', error);
        });
    };

    const signInDemo = () => {
      signInAnonymously(authentication)
        .then((result) => {
          console.log('Demo sign-in success', result);
          isLoggedIn.value = true;
          props.toggle();
        })
        .catch((error) => {
          console.error('Demo sign-in error', error);
        });
    };

    return {
      isLoggedIn,
      signInWithGoogle,
      signInWithGithub,
      signInDemo,
    };
  },
};
</script>

<style scoped>
#signinmodal {
    width: 100vw;
    height: 100vh;
    position: fixed;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    background-color: rgba(0, 0, 0, 0.7);
}

#signinmodal-child {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;

    background-color: #161616;
    padding: 10px;
    border-radius: 10px;
    color: white;
    border-right: 4px solid #ea1538;
    border-bottom: 4px solid #ea1538;
    text-align: center;
}

#signin-buttons > button {
    border: none;
    height: 50px;
    width: 240px;
    border-radius: 1px;
    font-size: medium;
    transition: background-color 0.218s ease 0s, border-color 0.218s ease 0s, box-shadow 0.218s ease 0s;
    margin: 5px;
}

#demo {
    background-color: #ea1538;
    color: white;
    box-shadow: rgb(0 0 0 / 25%) 0px 2px 4px 0px;
}

#demo:hover {
    cursor: pointer;
    box-shadow: rgba(232, 65, 93, 0.3) 0px 0px 3px 3px;
}

#nevermind-link {
    padding: 30px;
    color: red;
    text-decoration: none;
}

#nevermind-link:hover {
    cursor: pointer;
}

#signin-buttons {
    margin-top: 20px;
}

#signin-buttons > div {
    color: rgb(255, 255, 255);
    height: 50px;
    width: 240px;
    border: none;
    text-align: center;
    font-size: 16px;
    line-height: 48px;
    display: block;
    border-radius: 1px;
    transition: background-color 0.218s ease 0s, border-color 0.218s ease 0s, box-shadow 0.218s ease 0s;
    font-family: Roboto, arial, sans-serif;
    cursor: pointer;
    user-select: none;
    margin: 10px;
}

#google-child {
    width: 48px;
    height: 48px;
    text-align: center;
    /* background-color: #161616; */
    display: block;
    margin-top: 1px;
    margin-left: 1px;
    float: left;
    border-radius: 1px;
    white-space: nowrap;
}

#github-child {
    width: 48px;
    height: 48px;
    text-align: center;
    /* background-color: #161616; */
    display: block;
    margin-top: 1px;
    margin-left: 1px;
    float: left;
    border-radius: 1px;
    white-space: nowrap;
}

#github {
    background-color: rgb(32, 32, 32);
    box-shadow: rgba(0, 0, 0, 0.25) 0px 2px 4px 0px;
}

#google {
    background-color: rgb(14, 99, 234);
    box-shadow: rgba(0, 0, 0, 0.25) 0px 2px 4px 0px;
}
#github:hover {
    box-shadow: rgba(70, 70, 70, 0.3) 0px 0px 3px 3px;
}
</style>
