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
      <input class="action-item" type="text" v-model="item" />

      <md-button type="submit" class="md-icon-button submit-button">
        <md-icon>arrow_forward</md-icon>
      </md-button>
    </form>
  </div>
</template>
<style scoped>
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

.main-form {
  display: flex;
  align-items: flex-start;
  flex-direction: column;
  width: 80vw;
  position: relative;
}

form {
  text-align: left;
  display: flex;
  flex-direction: column;
  width: 100%;
}

.submit-button {
  position: absolute;
  right: 0;
  bottom: 10px;
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
