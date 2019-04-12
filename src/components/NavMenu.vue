<template>
  <div class="modal-bg" @click="onClose">
    <ul class="menu">
      <li
        @click="goto(item)"
        v-for="(item, index) in navItems"
        :key="index"
        class="nav-item"
      >
        {{ item }}
      </li>
      <li
        @click="logout"
        class="logout-link"
      >
        logout
      </li>
    </ul>
  </div>
</template>

<style scoped>
.modal-bg {
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: #00000066;
  display: flex;
  justify-content: center;
  align-items: center;
}
.menu {
  width: 70%;
  height: 60%;
  background-color: white;
  z-index: 100;
  border-radius: 10px;
  box-shadow: 1px 1px 18px 0 #00000050;
  padding: 20px;
  overflow: scroll;
}
.nav-item {
  list-style-type: none;
  font-size: xx-large;
  padding: 20px;
}
.nav-item:hover {
  cursor: pointer;
  background-color: lightgrey;
  transition: all ease 0.2s;
}
.logout-link{
  border-top: 1px lightgrey solid;
  padding: 20px;
  padding-top: 40px;
  margin-top: 20px;
  list-style-type: none;
  font-size: x-large;
}
.logout-link:hover{
  cursor: pointer;
  color: lightgrey;
  transition: all ease 0.2s;
}
</style>

<script lang="ts">
import Vue from "vue";
import { db, provider } from "../main";
import firebase from "firebase";
import "vue-material/dist/vue-material.min.css";
import { MdButton, MdIcon } from "vue-material/dist/components";

export default Vue.extend({
  name: "NavMenu",
  props: {},
  data() {
    return {
      navItems: []
    };
  },
  methods: {
    goto(item) {
      this.$router.push(`/${item.toLowerCase()}`);
    },
    onClose() {
      this.$emit("clicked");
    },
    logout() {
      firebase
        .auth()
        .signOut()
        .then(() => {
          console.log("logout success");
          this.$router.push('/');
        })
        .catch(err => {
          console.log("error " + err.message);
        });  
    }
  },
  created() {
    this.uid = firebase.auth().currentUser.uid;
    const userRef = db.collection("users").doc(`${this.uid}`);
    userRef.get().then(doc => {
      this.navItems = Object.keys(doc.data());
    });
  }
});
</script>
