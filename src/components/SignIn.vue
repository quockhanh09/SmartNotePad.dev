<template>
  <div id="signIn">
    <h1>Sign In!</h1>
    <p>To make posts on SmartNotePad, you are required to create an account. We support Google, Github, and a <strong>Demo Account</strong>.</p>
  </div>
</template>

<script>

import './styles/Responsive.css'
export default {
  name: 'SignIn',
  props: {
    toggle: {
      type: Boolean,
      required: false,
    },
  },
};
</script>

<style>
#signIn {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    color: white;
    background-color: #673AB7;
    padding-bottom: 15px;
}
#signIn h1 {
    margin-bottom: 10px;
}
p {
    margin: 5px;
}
#signIn p span {
    color: #F44336;
    font-weight: bold;
}

#signIn p span:hover {
    text-decoration: underline;
    cursor: pointer;
}
</style>
