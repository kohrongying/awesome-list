<template>
  <div id="app">
    <fragment v-if="authUser">
      <router-view :key="$route.path" />
      <NavButton @clicked="handlePress" :open="open"/>
      <NavMenu v-if="open" @clicked="handlePress" />
    </fragment>

    <fragment v-else>
      <LoginButton />
    </fragment>
  </div>
</template>

<style>
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
import { db } from "./main";
import NavButton from "@/components/NavButton.vue"; // @ is an alias to /src
import NavMenu from "@/components/NavMenu.vue";
import { Fragment } from "vue-fragment";

export default Vue.extend({
  name: "App",
  components: {
    LoginButton,
    NavButton,
    NavMenu,
    Fragment
  },
  data() {
    return {
      authUser: "",
      open: false
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
  },
  methods: {
    handlePress() {
      this.open = this.open ? false : true;
    }
  }
});
</script>
