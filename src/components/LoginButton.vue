<template>
  <div>
    <button class="login" @click="login">
      <h1>Login</h1>
      <md-button type="submit" class="md-icon-button">
        <md-icon>arrow_forward</md-icon>
      </md-button>
    </button>
  </div>
</template>

<style>
button.login {
  border: none;
  display: flex;
  flex-direction: row;
  align-items: center;
}

button.login:hover {
  cursor: pointer;
}
</style>

<script lang="ts">
import Vue from "vue";
import { db, provider } from "../main";
import firebase from "firebase";
import "vue-material/dist/vue-material.min.css";
import { MdButton, MdIcon } from "vue-material/dist/components";

export default Vue.use(MdButton)
  .use(MdIcon)
  .extend({
    name: "LoginButton",
    data() {
      return {
        authUser: ""
      };
    },
    methods: {
      login() {
        firebase
          .auth()
          .signInWithPopup(provider)
          .then(user => {
            console.log("hello");
            alert("login success");
          })
          .catch(err => {
            alert("error " + err.message);
          });
        console.log("end");
      }
    }
  });
</script>
