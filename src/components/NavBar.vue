<template>
    <div id="hero">
      <nav>
        <h2 class="logo">Smart<span>NotePad</span></h2>
        <h1 class="subhero">Home Page</h1>
        <template v-if="logged_in">
          <div id="user-logged" @click="signOut">
            <img
              :src="userPhotoURL ? userPhotoURL : anonymous"
              id="user_account"
              rel="noreferrer"
              alt="Your Avatar"
            />
            <h2>{{ userDisplayName ? userDisplayName : 'Demo User' }}</h2>
          </div>
        </template>
        <template v-else>
          <button type="button" @click="toggle">Login</button>
        </template>
      </nav>
    </div>
  </template>
  
  <script>
  // import { authentication } from "../services/firebase-config";
  import { authentication } from '../services/firebase-config';
  import './styles/Responsive.css'
  
  export default {
    props: {
      logged_in: Boolean,
      toggle: Function
    },
    
    computed: {
      userDisplayName() {
        return authentication.currentUser?.displayName;
      },
      userPhotoURL() {
        return authentication.currentUser?.photoURL;
      }
    },
    methods: {
      signOut() {
        if (authentication.currentUser) {
          authentication.signOut();
        }
      }
    }
  };
  </script>
  
  <style scoped>
 * {
  box-sizing: border-box;
  font-family: 'Josefin Sans', sans-serif;
}

nav {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding-left: 10%;
  padding-right: 10%;
}

.logo {
  color: white;
  font-size: 28px;
}

.logo span {
  color: #ea1538;
}

nav ul li {
  list-style-type: none;
  display: inline-block;
  padding: 10px 20px;
}

nav ul li a {
  color: white;
  text-decoration: none;
  font-weight: bold;
}

nav ul li a:hover {
  color: #ea1538;
  transition: .3s;
}

nav > button {
  border: none;
  background: #ea1538;
  padding: 12px 30px;
  border-radius: 30px;
  color: white;
  font-weight: bold;
  font-size: 15px;
  transition: .4s;
}

nav > button:hover {
  transform: scale(1.03);
  cursor: pointer;
}

.subhero {
  color: white;
}

#user_account {
  border-radius: 50%;
  padding: 10px;
}

#user-logged {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: row;
  color: white;
  padding: 10px;
}

#user-logged:hover {
  background-color: rgba(0, 0, 0, 0.4);
  cursor: pointer;
}


  </style>
  