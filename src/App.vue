<template>
  <div id="app">
    <fragment v-if="authUser">
      <router-view :key="$route.path" />
      <div class="nav-button-container">
        <NavButton />
      </div>
    </fragment>
    <fragment v-else>
      <LoginButton />
    </fragment>
  </div>
</template>

<style>
.nav-button-container {
  position: absolute;
  width: 100%;
  height: 100%;
  display: flex;
  align-items: flex-end;
  justify-content: center;
}
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  width: 100vw;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}

i {
  font-family: "Material Icons";
}
</style>

<script lang="ts">
import Vue from "vue";
import LoginButton from "@/components/LoginButton.vue";
import firebase from "firebase";
import NavButton from "@/components/NavButton.vue"; // @ is an alias to /src
import { Fragment } from "vue-fragment";

export default Vue.extend({
  name: "App",
  components: {
    LoginButton,
    NavButton,
    Fragment
  },
  data() {
    return {
      authUser: ""
    };
  },
  created() {
    firebase.auth().onAuthStateChanged(user => {
      if (user) {
        this.authUser = user.uid;
      } else {
        this.authUser = ""
      }
    });
  }
});
</script>
