<template>
  <div class="main-form">
    <div class="header">I wanna</div>
    <form @submit.prevent="addAction">
      <input
        autofocus
        class="action"
        type="text"
        placeholder="read"
        v-model="action"
      />
      <div class="input-wrapper">
        <input class="action-item" type="text" v-model="item" />
        <md-button type="submit" class="md-icon-button">
          <md-icon>arrow_forward</md-icon>
        </md-button>
      </div>
    </form>
  </div>
</template>
<style>
.main-form {
  padding: 0 180px;
  display: flex;
  align-items: flex-start;
  flex-direction: column;
}
form {
  text-align: left;
  display: flex;
  flex-direction: column;
}
</style>
<script lang="ts">
import Vue from "vue";
import "vue-material/dist/vue-material.min.css";
import { MdButton, MdIcon } from "vue-material/dist/components";
import { db } from "../main";
import firebase from "firebase";
import { Fragment } from "vue-fragment";

export default Vue.use(MdButton)
  .use(MdIcon)
  .extend({
    name: "Main",
    components: { Fragment },
    data() {
      return {
        action: "",
        item: "",
        uid: ""
      };
    },
    methods: {
      addAction() {
        const userRef = db.collection("users").doc(`${this.uid}`);
        userRef.update({
          [`${this.action
            .toLowerCase()
            .trim()}`]: firebase.firestore.FieldValue.arrayUnion({
            name: this.item,
            dateCreated: new Date(),
            status: "active"
          })
        });
        this.action = "";
        this.item = "";
      }
    },
    created() {
      const user = firebase.auth().currentUser;
      this.uid = user.uid;
    }
  });
</script>

<style scoped>
.container {
  display: flex;
  justify-content: center;
  padding-top: 100px;
}

.main {
  width: 50%;
  text-align: left;
}

.header {
  font-size: 40px;
  margin-top: 20px;
}

input {
  border: none;
  font-size: 40px;
  border: none;
  border-bottom: 1px #2c3e50 solid;
  color: #2c3e50;
  margin-top: 20px;
}

input:focus {
  outline: none;
}

.input-wrapper {
  display: flex;
  align-items: flex-end;
}

</style>